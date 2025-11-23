---
description: >-
  Desglosamos los módulos de Metasploit: Exploits, Payloads, Auxiliary y más.
  Aprende qué hace cada uno y dónde encontrarlos en el árbol de directorios de
  Kali Linux.
---

# Entendiendo los Módulos Clave de Metasploit

Ahora que ya sabes inicializar Metasploit Framework y conoces los conceptos de _Exploit_ y _Payload_, es momento de sumergirnos en la arquitectura que hace de esta herramienta una plataforma tan poderosa y versátil: sus Módulos.

Si alguien te pregunta qué es Metasploit, la respuesta más precisa es: "Metasploit es una colección masiva de módulos."

Todo lo que haces dentro del _Framework_ es a través de un módulo. Entender el propósito de cada uno te permite planear y ejecutar una prueba de penetración de forma metódica y profesional.

***

## <mark style="color:yellow;">1. ¿Qué es un Módulo?</mark>

Un módulo en Metasploit es una pieza de código independiente y auto-contenida que está diseñada para ejecutar una tarea muy específica. Esta tarea puede ser técnica, como explotar una vulnerabilidad; de reconocimiento, como escanear un puerto; o de post-explotación, como recolectar credenciales.

A continuación, te presentamos las categorías principales que componen el _Framework_:

***

## <mark style="color:yellow;">2. Los Módulos Centrales de Metasploit</mark>

Estos son los pilares sobre los que se construye cualquier prueba de penetración:

#### <mark style="color:green;">A. Exploits (La Puerta de Entrada)</mark>

* Propósito: Contienen el código que aprovecha una vulnerabilidad específica en un sistema, aplicación o servicio. Su meta es conseguir un punto de entrada.
* Ejemplo: Un módulo de _exploit_ diseñado para aprovechar un fallo de ejecución remota de código (RCE) en una versión antigua de un servidor web.

#### <mark style="color:green;">B. Payloads (La Ejecución de la Tarea)</mark>

* Propósito: Es el código que se envía y se ejecuta en el sistema víctima _después_ de que el _exploit_ ha logrado la entrada.
* Ejemplo: `meterpreter` (un _payload_ avanzado que ofrece una interfaz de control poderosa), _shells_ (conexiones de consola simples), o _payloads_ que añaden usuarios.

#### <mark style="color:green;">C. Auxiliary (El Soporte y Reconocimiento)</mark>

* Propósito: Son herramientas de soporte que no tienen como objetivo la explotación directa, sino tareas de apoyo. Son vitales en la fase de reconocimiento e información.
* Ejemplo: Módulos para escaneo de puertos, _sniffing_, detección de servicios o ataques de fuerza bruta (_brute-force_).

#### <mark style="color:green;">D. Post (La Persistencia y Movimiento)</mark>

* Propósito: Módulos que se usan después de que la explotación inicial fue exitosa y ya tienes una sesión activa en la máquina víctima (_post-explotación_). Su objetivo es la escalada de privilegios, el movimiento lateral o la recolección de datos sensibles.
* Ejemplo: Módulos para _dumping_ de _hashes_ de contraseñas de Windows o para obtener información de configuración de red.

***

## <mark style="color:yellow;">3. Módulos de Soporte (El Arte de la Evasión)</mark>

Estos módulos tienen una función muy específica: hacer que la explotación sea exitosa sin ser detectada.

#### <mark style="color:green;">A. Encoders (El Ofuscador)</mark>

* Propósito: Se utilizan para ofuscar el _payload_ (hacer que parezca ilegible) con el fin de evadir la detección básica de _signatures_ de antivirus. No es encriptación fuerte, sino una transformación simple.
* Importancia Educativa: Entender su funcionamiento es clave para comprender cómo el antivirus basado en firmas (detección simple) puede ser eludido.

#### <mark style="color:green;">B. Nops (No-Operation Instructions)</mark>

* Propósito: Son secuencias de pequeñas "instrucciones de no-operación" (_No-Operation Instructions_) que se añaden antes del _payload_ para estabilizar ciertos _exploits_ (especialmente los basados en desbordamientos de búfer) y asegurar que el código se ejecute correctamente.

#### <mark style="color:green;">C. Evasion (La Técnica Activa)</mark>

* Propósito: Técnicas activas destinadas a evadir sistemas de seguridad más avanzados como _Endpoint Detection and Response_ (EDR) o antivirus de última generación.

***

## <mark style="color:yellow;">4. Dónde Viven los Módulos: El Árbol de Directorios en Kali Linux</mark>

Si quieres examinar el código de un módulo, modificarlo, o simplemente ver cómo está organizada la estructura de Metasploit, necesitas saber dónde buscar.

En la mayoría de las instalaciones estándar de Kali Linux, los módulos de Metasploit Framework se encuentran ubicados en el siguiente directorio:

> Ruta Principal de Módulos:
>
> /usr/share/metasploit-framework/modules/

Dentro de ese directorio, verás subcarpetas que corresponden exactamente a las categorías que acabamos de describir:

| **Categoría de Módulo** | **Subdirectorio en Kali Linux**                      |
| ----------------------- | ---------------------------------------------------- |
| Exploits                | `/usr/share/metasploit-framework/modules/exploits/`  |
| Payloads                | `/usr/share/metasploit-framework/modules/payloads/`  |
| Auxiliary               | `/usr/share/metasploit-framework/modules/auxiliary/` |
| Post                    | `/usr/share/metasploit-framework/modules/post/`      |
| Encoders                | `/usr/share/metasploit-framework/modules/encoders/`  |

Consejo: Revisar estos directorios y leer el código fuente (código Ruby) de los módulos que usas te dará una comprensión mucho más profunda de lo que realmente está haciendo la herramienta.
