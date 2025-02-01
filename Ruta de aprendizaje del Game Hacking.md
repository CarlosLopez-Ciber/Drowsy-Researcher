# Ruta de aprendizaje del Game Hacking

> Debido a que no encontraba una ruta clara de aprendizaje sobre el Game Hacking, decidí crear esta ruta con ayuda del NotebookLM, una IA que te permite resumir información de recursos que uno le adjunte. Al final de toda esta publicación, adjunto la información de los recursos utilizados para el desarrollo de la presente ruta de aprendizaje.

## 1. Fundamentos de Programación

- **C++: El Lenguaje Predilecto**
    - **C++ es altamente recomendado** para el game hacking debido a su capacidad para la manipulación de memoria de bajo nivel. Esta capacidad es crucial ya que permite a los hackers acceder y modificar directamente la memoria donde los juegos almacenan información vital como la salud del jugador, la munición, etc..
    - Es un lenguaje **compilado**, lo que significa que el código se traduce directamente a instrucciones de máquina, resultando en un **alto rendimiento**, una característica esencial para el desarrollo de cheats que deben operar en tiempo real sin causar retrasos.
    - La mayoría de los **motores de juegos** y los propios juegos están escritos en C++, lo que lo convierte en el estándar de la industria para videojuegos. Esto implica que un conocimiento profundo de C++ te permitirá entender mejor cómo funcionan los juegos y cómo interactuar con ellos.
    - Aunque se considera un lenguaje difícil al principio debido a su complejidad, su poder y flexibilidad lo convierten en la mejor herramienta para el game hacking.
    - Se recomienda aprender C++ a través de recursos como **learncpp.com**, que ofrece tutoriales basados en texto, o la serie de videos de **Cherno** en YouTube.
    - Se necesita un buen dominio de C++ para usar la API de Windows, la cual es fundamental para el game hacking.
    - Es importante destacar que C++ es el lenguaje más adecuado para escribir el código central de un bot (hooks, lectura de memoria) mientras se hace uso de Lua (un lenguaje de alto nivel) para la automatización.
- **Python: Un Buen Punto de Partida**
    - Python se presenta como una alternativa para los principiantes debido a su **sintaxis más sencilla y su curva de aprendizaje menos pronunciada**.
    - Al ser un lenguaje de más alto nivel, permite obtener resultados gratificantes más rápidamente, lo que puede aumentar la motivación de los nuevos programadores.
    - A pesar de que C++ es el lenguaje de elección para el game hacking, Python puede ser útil para el **desarrollo de bots fuera del juego**, especialmente en lo relacionado con la programación de redes.
    - La experiencia con Python puede facilitar el regreso a C++ con una perspectiva nueva y mayor comprensión de los conceptos de programación.
- **Conceptos Fundamentales de Programación**
    - Es esencial tener un manejo sólido de los **conceptos básicos de programación**, que incluyen:
        - **Funciones**: Bloques de código que realizan tareas específicas y son reutilizables.
        - **Control de Flujo**: Estructuras como condicionales (if, else) y bucles (for, while) que dirigen la ejecución del programa.
        - **Punteros**: Variables que almacenan direcciones de memoria, cruciales para la manipulación directa de memoria en C++.
        - **Clases**: Plantillas para crear objetos, fundamentales en la programación orientada a objetos, que es común en el desarrollo de juegos.
- **Lenguaje Ensamblador (ASM): La Base del Reverse Engineering**
    - **Aprender a leer ASM es fundamental** para el game hacking, ya que permite entender el código a nivel de máquina y cómo el juego interactúa directamente con el hardware del ordenador.
    - El código de ensamblaje es la forma en que las computadoras entienden las instrucciones de un programa. Con el conocimiento de ASM, se puede ver la versión de bajo nivel del código que se ejecuta en la computadora, lo cual es muy útil para el game hacking.
    - Al reversear un programa, los hackers a menudo interactúan con el código de ensamblaje.
    - No es necesario convertirse en un experto en la escritura de ASM, pero se debe poder leer e interpretar el código para comprender el funcionamiento interno de un programa.
    - Herramientas como **OllyDbg**, **x64dbg** e **IDA Pro** permiten analizar el código ensamblador.
    - La habilidad para leer ASM también es útil para entender técnicas como NOPing y hooking.
    - Se recomienda practicar revirtiendo programas propios en C++ para comprender cómo el código de alto nivel se traduce a ASM.
    - Hay varios recursos en línea para aprender ensamblador.

## 2. Reverse Engineering (Ingeniería Inversa)

- El **reverse engineering** es un proceso fundamental en el game hacking que implica **desarmar un programa (como un videojuego) para entender cómo funciona internamente**. Esto es crucial porque los hackers de juegos no tienen acceso al código fuente original del juego. En lugar de eso, trabajan con el código compilado (binario) que es difícil de entender directamente. La finalidad es **descubrir vulnerabilidades y comprender la lógica del juego**, lo cual es esencial para desarrollar hacks o bots.
    
- **Propósito del Reverse Engineering**:
    
    - **Comprender la estructura y el flujo de ejecución del juego**.
    - **Identificar la ubicación de variables importantes en la memoria** (como salud, munición, posición, etc.).
    - **Descubrir funciones, clases y variables** útiles para la manipulación del juego.
    - **Encontrar vulnerabilidades** para explotarlas y crear hacks.
    - **Reconstruir la lógica del programa** y entender cómo interactúa con el sistema y la red.
    - **Crear herramientas personalizadas** para el análisis y la manipulación del juego.
- **Tipos de Análisis en el Reverse Engineering:**
    
    - **Análisis Estático:** Este tipo de análisis se realiza **sin ejecutar el programa**. Consiste en examinar el código binario, su estructura, las bibliotecas que utiliza y otros aspectos del archivo.
        
        - Se inspecciona el código ensamblador para entender la lógica del programa.
        - Se identifican cadenas de texto (strings) que pueden dar pistas sobre la funcionalidad del programa.
        - Se analiza la información del encabezado del archivo (como el formato PE en Windows) para comprender sus dependencias y características.
        - Se utilizan herramientas como desensambladores y analizadores de archivos PE para examinar el código sin ejecutarlo.
        - Permite **identificar posibles vulnerabilidades** sin los riesgos asociados con la ejecución del código.
        - Es un punto de partida para el análisis, ya que la información estática se puede obtener rápidamente sin ejecutar el programa.
        - En el análisis de malware, la información estática ayuda a identificar infraestructura maliciosa o archivos comprimidos.
    - **Análisis Dinámico:** Este tipo de análisis se realiza **ejecutando el programa en un entorno controlado** (como una máquina virtual). Se observa el comportamiento del programa durante la ejecución para entender su funcionamiento.
        
        - Se utilizan **depuradores** para controlar la ejecución del programa línea por línea, observar cambios en la memoria y en los registros, y establecer puntos de interrupción (breakpoints).
        - Permite identificar cómo el programa interactúa con el sistema (archivos, registro, red).
        - Se utiliza para confirmar funcionalidades y manejar encriptación o payloads.
        - Permite **descubrir la lógica de un algoritmo** o funciones ocultas del programa.
        - Ayuda a encontrar **caminos de punteros a memoria dinámica**.
        - En el análisis de malware, se utiliza para observar el comportamiento malicioso y cómo evade el sandbox.
- **Análisis Híbrido**: Combina técnicas de análisis estático y dinámico para obtener una visión más completa, ya que algunos malwares ocultan su presencia y pueden ser detectados usando análisis hibrido.
    
- **Herramientas Clave para el Reverse Engineering:**
    
    - **Desensambladores:**
        - **IDA Pro:** Es una herramienta muy popular en la industria de la seguridad, conocida por su capacidad de desensamblar código en diferentes arquitecturas (x86, ARM). Permite generar diagramas de flujo, tiene scripting, y con su plugin Hex-Rays, puede incluso generar código C equivalente. Existe una versión gratuita limitada. Es considerado uno de los mejores desensambladores y decompiladores en el mercado.
        - **Ghidra:** Es una alternativa **gratuita y de código abierto** mantenida por la NSA. Ofrece capacidades similares a IDA Pro, incluyendo desensamblado, decompilación y scripting. Es una herramienta potente para analizar código compilado.
        - **Hopper:** Un desensamblador para macOS y Linux.
        - **Radare2:** Un framework de reverse engineering que actúa como herramienta forense, editor hexadecimal, analizador binario, desensamblador y depurador.
    - **Depuradores:** Permiten la **ejecución controlada del programa** para observar su comportamiento en tiempo real.
        - **x64dbg:** Es un depurador de código abierto para Windows, que puede depurar aplicaciones de 32 y 64 bits. Es muy popular entre los hackers de juegos.
        - **OllyDbg:** Es un depurador a nivel de ensamblador muy útil para el análisis de juegos. Es conocido por su portabilidad y variedad de funciones. Puede ser extendido con plugins para capacidades adicionales.
        - **WinDbg:** Es el depurador oficial de Microsoft para Windows, útil para depurar tanto código de usuario como del kernel. Puede cargar volcados de memoria y símbolos para facilitar el análisis.
        - **GDB (GNU Debugger):** Depurador originalmente para Linux, pero también usado para Windows. Soporta lenguajes de alto nivel como C, C++, y Java.
        - **Immunity Debugger:** Una versión mejorada de OllyDbg con soporte para plugins en Python.
    - **Herramientas de Análisis de Memoria:**
        - **Cheat Engine:** Es una herramienta versátil para **escanear y modificar la memoria de un juego**. También incluye un depurador y un desensamblador básicos. Es ideal para principiantes debido a su facilidad de uso. Permite crear tablas de trucos (cheat tables) que pueden ser compartidas con otros usuarios.
        - **ReClass.NET:** Se utiliza para visualizar y **reconstruir estructuras de datos en la memoria**, mostrando cómo los bytes se interpretan en diferentes tipos de datos. Es útil para organizar y entender grandes bloques de memoria.
    - **Otras Herramientas:**
        - **HxD:** Un editor hexadecimal básico.
        - **CFF Explorer:** Un visualizador de archivos PE que extrae información importante de los ejecutables.
        - **Process Monitor y Process Explorer:** Herramientas que permiten monitorear las acciones de un proceso, como interacciones con archivos, registros, y otros procesos.
- **Técnicas de Anti-Reverse Engineering**: Los creadores de software (incluidos los malwares) utilizan técnicas para dificultar el proceso de reverse engineering. Algunas de estas técnicas incluyen:
    
    - **Ofuscación de código**: Hace que el código sea más difícil de entender.
    - **Anti-depuración**: Detecta cuando se ejecuta el programa en un depurador y altera su comportamiento.
    - **Anti-desensamblado**: Utiliza trucos que confunden a los desensambladores, ocultando instrucciones válidas.
    - **Encriptación**: El malware puede encriptar su propio código o datos.
- **Importancia del Conocimiento de Ensamblador**: Para un análisis exhaustivo, es necesario entender el lenguaje ensamblador. El desensamblador convierte el código máquina en mnemónicos de ensamblador, y es imprescindible aprender a leer el código ensamblador para entender lo que realmente hace el software a nivel bajo.

## 3. Manipulación de Memoria

- **Concepto Fundamental:** La manipulación de memoria es una técnica esencial en el game hacking que implica **leer y escribir datos en la memoria de un proceso en ejecución (específicamente un videojuego)**. La memoria de un juego contiene una representación numérica del estado del juego, como la salud del jugador, la posición, la cantidad de dinero, etc. Los hackers usan la manipulación de memoria para alterar estos valores y así modificar la jugabilidad.
    
- **Objetivos de la Manipulación de Memoria:**
    
    - **Encontrar y modificar valores del juego**: Localizar la dirección de memoria donde se almacenan datos como la salud, munición o puntuación, y cambiar estos valores.
    - **Crear trucos y hacks**: Automatizar acciones, como aumentar la salud, la munición, o teletransportarse por el mapa.
    - **Desarrollar bots**: Programas que pueden jugar automáticamente, realizando tareas como curarse, atacar o recolectar recursos.
    - **Comprender el estado del juego**: Obtener una representación numérica de las variables del juego que permita interactuar con él de manera inteligente.
    - **Personalizar la experiencia del juego**: Permitir a los jugadores modificar aspectos del juego a su gusto.
- **Herramientas Principales para la Manipulación de Memoria:**
    
    - **Cheat Engine**: Es una herramienta de código abierto muy utilizada para la manipulación de memoria en juegos. Permite:
        - **Escanear la memoria:** Buscar valores específicos en la memoria de un proceso.
        - **Modificar valores en tiempo real:** Alterar directamente los datos encontrados en la memoria.
        - **Crear cheat tables:** Guardar direcciones de memoria y sus valores para futuras sesiones.
        - **Generar trainers:** Automatizar la modificación de valores a través de atajos de teclado.
        - **Realizar escaneo de punteros:** Encontrar cadenas de punteros que apuntan a direcciones de memoria dinámicas.
        - **Utilizar Lua Scripting:** Automatizar tareas complejas de manipulación de memoria mediante scripts.
    - **OllyDbg:** Un depurador a nivel de ensamblador que permite un análisis más profundo de la memoria del juego. Facilita la identificación de punteros mediante la traza de ejecución y permite examinar el código de ensamblador del juego.
    - **ReClass.NET:** Permite visualizar bloques de memoria como tipos de datos, facilitando la reconstrucción de estructuras de datos.
    - **Process Monitor y Process Explorer:** Permiten monitorizar las acciones de un proceso, incluyendo interacciones con la memoria, facilitando la identificación de áreas de interés en la memoria.
- **Proceso de Escaneo de Memoria con Cheat Engine:**
    
    1. **Adjuntar Cheat Engine al proceso del juego:** Seleccionar el proceso del juego al que se quiere modificar la memoria.
    2. **Realizar un primer escaneo (First Scan):** Buscar en la memoria del proceso valores que coincidan con un valor conocido. Por ejemplo, si conoces tu cantidad de salud actual (ejemplo: 100), buscas el valor 100.
    3. **Filtrar los resultados (Next Scan):** Cambiar el valor buscado en el juego (por ejemplo, dañar al personaje para que su salud cambie), luego realizar un nuevo escaneo para encontrar las direcciones de memoria que cambiaron su valor. Este proceso se repite hasta encontrar la dirección de memoria que se necesita.
    4. **Determinar la dirección correcta:** En algunos casos, es necesario experimentar modificando manualmente los valores de las direcciones restantes hasta encontrar la que afecta al valor buscado.
    5. **Añadir la dirección a la cheat table:** Guardar las direcciones encontradas y sus valores para facilitar su uso futuro.
    6. **Modificar la memoria:** Cambiar el valor guardado en la cheat table directamente, o crear un trainer para automatizar la modificación.
    7. **Congelar (freeze) valores:** Asegurar que un valor no cambie, escribiendo el mismo valor de manera repetitiva en la dirección de memoria.
- **Tipos de Escaneo:** Cheat Engine permite diferentes tipos de escaneo, incluyendo:
    
    - **Exact Value:** Busca valores que coinciden exactamente con el valor ingresado.
    - **Increased Value:** Busca valores que han aumentado desde el escaneo anterior.
    - **Decreased Value:** Busca valores que han disminuido desde el escaneo anterior.
    - **Value Between:** Busca valores que están dentro de un rango específico.
    - **Unknown Initial Value:** Busca valores cambiados sin saber su valor previo.
- **Direcciones Estáticas vs. Dinámicas:**
    
    - **Direcciones Estáticas:** Son direcciones de memoria que permanecen constantes durante la ejecución del juego y entre sesiones. Estas direcciones son ideales para crear hacks duraderos, ya que no cambian. Las direcciones estáticas suelen estar en color verde en Cheat Engine.
    - **Direcciones Dinámicas:** Son direcciones de memoria que cambian cada vez que se inicia el juego. Para acceder a estos valores, se utilizan punteros y escaneo de punteros. Las direcciones dinámicas suelen estar en color negro en Cheat Engine.
- **Escaneo de Punteros (Pointer Scanning):**
    
    - Los **punteros** son direcciones de memoria que apuntan a otras direcciones. Un **pointer chain (cadena de punteros)** es una serie de punteros que, al seguirse uno tras otro, llevan a la dirección de memoria que contiene un valor de interés.
    - El **escaneo de punteros** permite encontrar estas cadenas de punteros que llevan a direcciones dinámicas de memoria. Esto es crucial en juegos que almacenan valores en memoria de forma dinámica.
    - Para realizar un escaneo de punteros en Cheat Engine, se hace clic derecho en una dirección dinámica y se elige "Pointer scan for this address".
    - Cheat Engine ofrece diversas opciones para optimizar el escaneo de punteros, incluyendo limitar la longitud de la cadena, buscar solo punteros estáticos, y evitar direcciones de solo lectura.
- **Importancia de los Punteros**:
    
    - Los punteros son esenciales para acceder a la memoria dinámica, ya que estas direcciones cambian cada vez que se inicia el juego.
    - Permiten acceder a la información de una manera estable, siempre que el puntero inicial en la cadena de punteros sea estático.
- **Otros aspectos importantes de la manipulación de memoria**:
    
    - Los valores en memoria se guardan con tipos de datos específicos como enteros, flotantes, etc..
    - Las estructuras de datos organizan la información, y al entenderlas, se pueden manipular grandes bloques de memoria con una sola dirección.
    - Es crucial comprender la diferencia entre código y datos en la memoria.
    - Los juegos pueden usar técnicas de ofuscación para ocultar los valores en memoria.
    - La protección de memoria (como ASLR - Address Space Layout Randomization) dificulta la manipulación de memoria y requiere técnicas de bypass.

## 4. API de Windows (WinAPI)

- **Concepto Fundamental:** La API de Windows (WinAPI), también conocida como Win32 API, es un conjunto de **funciones y estructuras de datos** que proporciona el sistema operativo Windows para que los desarrolladores de software puedan interactuar con él. Estas APIs permiten a los programas realizar una amplia variedad de tareas, desde la gestión de memoria hasta la creación de interfaces gráficas de usuario, pasando por la comunicación en red y la manipulación de archivos. En el contexto del _game hacking_, la WinAPI es esencial porque ofrece las herramientas necesarias para **manipular procesos y memoria de otros programas**, incluyendo los videojuegos.
    
- **Importancia en el Game Hacking**: La WinAPI es fundamental para el _game hacking_ porque proporciona las funciones de bajo nivel necesarias para:
    
    - **Acceder y modificar la memoria de otros procesos**: Funciones como `ReadProcessMemory` y `WriteProcessMemory` permiten a los hackers leer y escribir datos en la memoria de otros procesos, lo que es esencial para modificar valores del juego.
    - **Inyectar código en otros procesos**: Funciones como `VirtualAllocEx` y `CreateRemoteThread` permiten a los hackers inyectar y ejecutar código en otros procesos, lo cual se utiliza para introducir _hacks_ o _bots_ en los juegos.
    - **Depurar procesos**: Las funciones de depuración de la WinAPI se pueden usar para analizar el comportamiento de un programa, detectar vulnerabilidades y entender cómo funciona internamente.
    - **Monitorear eventos**: Permite a los hackers monitorizar eventos del sistema, como pulsaciones de teclas o mensajes de ventanas, lo cual es útil para crear keyloggers o detectar acciones del usuario.
    - **Gestionar procesos y threads**: Permite a los hackers crear, manipular y finalizar procesos y threads, lo cual es fundamental para controlar cómo un programa interactúa con el sistema.
- **Funciones Clave de la WinAPI para Game Hacking**:
    
    - **`ReadProcessMemory`**: Permite leer datos desde una dirección específica en la memoria de otro proceso. Esta función toma como argumentos un _handle_ al proceso objetivo, la dirección de memoria a leer, un _buffer_ para almacenar los datos leídos y el tamaño de los datos a leer.
    - **`WriteProcessMemory`**: Permite escribir datos en una dirección específica en la memoria de otro proceso. Similar a `ReadProcessMemory`, esta función toma un _handle_ al proceso objetivo, la dirección de memoria a escribir, un _buffer_ con los datos a escribir y el tamaño de los datos a escribir.
    - **`VirtualAllocEx`**: Permite reservar memoria en la memoria virtual de otro proceso. Esencial para inyectar código, esta función toma un _handle_ al proceso objetivo, la dirección de inicio de la memoria, el tamaño de la memoria a reservar y el tipo de protección deseada.
    - **`CreateRemoteThread`**: Permite crear un nuevo hilo de ejecución en otro proceso. Esta función toma un _handle_ al proceso objetivo, un puntero a la función que el nuevo hilo ejecutará y argumentos para esta función. Se utiliza en la inyección de código para comenzar la ejecución del código inyectado.
    - **`OpenProcess`**: Permite obtener un _handle_ a un proceso en ejecución, necesario para usar otras funciones como `ReadProcessMemory`, `WriteProcessMemory` y `VirtualAllocEx`. Esta función toma como argumento el identificador del proceso (PID).
    - **`CloseHandle`**: Permite cerrar un _handle_ previamente abierto, liberando los recursos del sistema asociados a él. Es importante cerrar los _handles_ cuando ya no son necesarios para evitar fugas de memoria.
    - **`GetWindowThreadProcessId`**: Obtiene el ID del proceso asociado a una ventana especificada.
    - **`FindWindow`**: Obtiene el _handle_ de una ventana basada en su título. Se usa para obtener el _handle_ del juego y, a partir de él, obtener el PID.
    - **`GetProcAddress`**: Recupera la dirección de una función exportada desde una biblioteca de enlaces dinámicos (DLL). Se usa para obtener el punto de entrada de las funciones API.
    - **`LoadLibrary`**: Carga una DLL en el espacio de direcciones del proceso actual. Es usada frecuentemente para inyectar DLLs.
    - **`VirtualProtect`**: Cambia la protección de una región de memoria, por ejemplo, para permitir escribir en una región que originalmente era de solo lectura. Esencial para la inyección de código y la manipulación de memoria.
    - **`GetAsyncKeyState`**: Determina si una tecla está presionada. Es usada por los keyloggers para registrar las pulsaciones de teclas.
- **Funciones de Depuración, Toolhelp y Hooking**:
    
    - **Funciones de depuración**: La WinAPI proporciona funciones que permiten a un depurador controlar la ejecución de un proceso, establecer puntos de interrupción, inspeccionar variables, etc.. Estas funciones son fundamentales para el análisis de malware y el _reverse engineering_.
    - **Toolhelp Functions**: Son un conjunto de funciones que permiten enumerar y obtener información sobre los procesos, threads, módulos y _heaps_ en el sistema. Son útiles para obtener información sobre el estado del sistema y los recursos usados por un proceso.
    - **Funciones de Hooking**:
        - El _hooking_ (enganche) es una técnica que intercepta llamadas a funciones específicas (como funciones de la WinAPI), permitiendo al hacker ejecutar su propio código antes, después, o en lugar de la función original.
        - Esto se usa para registrar eventos, modificar el comportamiento de un programa o inyectar _malware_.
        - Los _hooks_ pueden ser locales (aplicados a un solo proceso) o globales (aplicados a todo el sistema).
        - Existen diferentes tipos de hooking:
            - **API Hooking**: Se basa en la modificación de la tabla de importación de direcciones (IAT) de un proceso.
            - **DLL Injection**: Se basa en inyectar una DLL en un proceso para cambiar su comportamiento. Una vez inyectada la DLL, esta puede actuar como una API que permite el acceso externo y la interacción con el proceso.
            - **Hooking con mensajes de bajo nivel**: Se basa en monitorizar mensajes del teclado y ratón a nivel del sistema operativo para registrar las acciones del usuario.
            - **Virtual Function (VF) Hooking**: Se basa en interceptar llamadas a funciones virtuales de clases para modificar su comportamiento.
- **Importancia de las DLLs (Dynamic-Link Libraries)**:
    
    - Las DLLs son bibliotecas de código que contienen funciones y recursos que pueden ser compartidos por múltiples programas.
    - La WinAPI se implementa principalmente a través de DLLs.
    - Las DLLs pueden ser cargadas dinámicamente por un proceso en tiempo de ejecución, lo que las convierte en un vector común para la inyección de código.
    - La inyección de DLLs permite modificar el comportamiento de un proceso desde dentro, ya que el código inyectado tiene acceso a la memoria y otros recursos del proceso.
- **Creación de Programas Básicos de Ventanas**:
    
    - Aprender a crear programas básicos de ventanas en Windows ayuda a comprender cómo funcionan los eventos y mensajes.
    - Los programas de ventanas envían y reciben mensajes que indican qué acciones debe realizar la aplicación (por ejemplo, cuando el usuario hace clic en un botón o escribe en un cuadro de texto).
    - Esta comprensión es útil para manipular la interfaz de un juego o para interceptar eventos que ocurren en él.
    - Para crear programas de ventanas, se usan las funciones de la WinAPI que manejan ventanas, como `CreateWindowExW`, `RegisterClassExW`, `ShowWindow`, y `UpdateWindow`.
- **Bibliotecas Comunes de la WinAPI:**
    
    - **KERNEL32.DLL**: Contiene funciones base del sistema, gestión de archivos, memoria, procesos y _threads_.
    - **USER32.DLL**: Contiene funciones para la gestión de la interfaz gráfica de usuario (ventanas, menús, mensajes, etc.).
    - **ADVAPI32.DLL**: Contiene funciones relacionadas con el registro de Windows y servicios.
    - **MSVCRT.DLL**: Contiene funciones estándar de la biblioteca de tiempo de ejecución de C, como `printf`, `scanf`, `malloc`, etc..
    - **WS2_32.DLL, WININET.DLL, URLMON.DLL, NETAPI32.DLL**: Contienen funciones para la comunicación en red e internet.
    - **NTDLL.DLL**: Contiene funciones nativas que interactúan directamente con el kernel del sistema.
- **Consideraciones Adicionales**:
    
    - La WinAPI está documentada en la MSDN Library (Microsoft Developer Network).
    - Es útil conocer los parámetros de cada función, sus valores de retorno y posibles errores.
    - La WinAPI puede ser utilizada desde diferentes lenguajes de programación que puedan manejar las estructuras de datos de bajo nivel.
    - Hay una gran cantidad de APIs no documentadas que son usadas por malware para esconder su comportamiento.

## 5. Inyección de Código y DLLs

- **Concepto General**: La inyección de código es una técnica que permite **ejecutar código arbitrario dentro del espacio de memoria de otro proceso**, como un videojuego. En el contexto del _game hacking_, esto significa que un hacker puede introducir su propio código en el juego, lo que le da un control significativo sobre el comportamiento del mismo. La inyección de DLLs es una forma común de lograr la inyección de código.
    
- **Importancia en el Game Hacking**:
    
    - La inyección de código es una técnica poderosa que permite a los _hackers_ modificar un juego desde adentro.
    - Al ejecutar código en el contexto del proceso del juego, el código inyectado puede acceder a la memoria del juego, a sus funciones internas y a otros recursos.
    - Esto permite realizar modificaciones muy complejas, como crear _bots_, modificar la jugabilidad o implementar funcionalidades adicionales.
    - La inyección de código también se puede utilizar para implementar _hacks_ que proporcionan ventajas injustas a los jugadores, como _wallhacks_ o _aimbots_.
    - La inyección de código puede ser utilizada con fines legítimos, como depurar o mejorar un juego.
- **Inyección de DLLs (Dynamic Link Libraries)**:
    
    - Las DLLs son archivos que contienen código y datos que pueden ser compartidos por múltiples programas.
    - La inyección de DLLs consiste en forzar a un proceso a cargar una DLL específica en su espacio de memoria.
    - Una vez que una DLL ha sido inyectada en un proceso, su código puede ser ejecutado dentro de ese proceso.
    - Esta técnica es comúnmente utilizada en _game hacking_ porque es más fácil escribir código en C++ y compilarlo como una DLL, que escribir código _shellcode_ a bajo nivel.
    - La DLL inyectada se convierte en parte del proceso objetivo, teniendo acceso a su memoria y recursos.
- **Métodos de Inyección de DLLs**:
    
    - **Uso de `LoadLibrary`**: Una forma común de inyectar una DLL es utilizando la función `LoadLibrary` de la WinAPI.
        - Un _hacker_ puede utilizar un _code cave_ para **llamar a la función `LoadLibrary`** dentro del proceso objetivo y forzarlo a cargar una DLL maliciosa.
    - **Thread Injection**: Se crea un nuevo hilo de ejecución en el proceso objetivo, el cual llama a la función `LoadLibrary` para cargar la DLL.
        - Se puede utilizar la función `CreateRemoteThread` para crear este nuevo hilo.
    - **Hijacking**: El hilo principal del proceso es modificado para que ejecute un _code cave_ que cargue la DLL.
        - El hilo principal es "congelado" y se redirecciona su ejecución al _code cave_ que ejecuta la función `LoadLibrary` para cargar la DLL.
- **Proceso de Inyección de Código (General)**:
    
    1. **Localizar el proceso objetivo**: El proceso en el cual se va a inyectar el código.
    2. **Obtener un _handle_ del proceso objetivo**: Se utiliza la función `OpenProcess` para obtener el _handle_.
    3. **Reservar memoria en el proceso objetivo**: Se utiliza la función `VirtualAllocEx` para reservar memoria en la memoria virtual del proceso objetivo.
    4. **Escribir el código (o la ruta de la DLL) en la memoria reservada**: Se utiliza la función `WriteProcessMemory` para copiar el código o la ruta de la DLL en la memoria reservada en el proceso objetivo.
    5. **Ejecutar el código inyectado**: Se utiliza `CreateRemoteThread` o `QueueUserAPC` para forzar al proceso objetivo a ejecutar el código inyectado.
- **Code Caves**:
    
    - Un _code cave_ es un fragmento de memoria dentro del proceso objetivo que contiene código de _shellcode_ que se utiliza para realizar acciones como la llamada a LoadLibrary.
    - Los _code caves_ pueden ser utilizados para inyectar código o para realizar modificaciones en el flujo de control del proceso.
- **Uso de un "Trainer"**:
    
    - Un _trainer_ es una herramienta que se utiliza para modificar los juegos, y a menudo utiliza la inyección de DLLs.
    - Un _trainer_ se adjunta al proceso de un juego y escucha las pulsaciones de teclas asociadas a la funcionalidad de las teclas de acceso rápido.
    - Cuando se detecta una pulsación de teclas, el _trainer_ ejecuta la funcionalidad asociada a través de la API del _backdoor_ de la DLL inyectada.
    - El _trainer_ puede inyectar una DLL que actúa como una API de _backdoor_ permitiendo modificar la memoria del juego o las funciones que el juego ejecuta.
    - Un _trainer_ puede ser guardado como un ejecutable portable que puede ser ejecutado después de que el juego ha sido lanzado para adjuntar el trainer al juego.
- **Consideraciones Importantes**:
    
    - La inyección de código es una técnica poderosa, pero también puede ser peligrosa si se utiliza con fines maliciosos.
    - Para inyectar código o DLLs, se requieren permisos elevados del sistema operativo, lo que puede ser un riesgo de seguridad si se utilizan herramientas de origen desconocido.
    - Es esencial tener precaución al utilizar _trainers_ o herramientas de _hacking_ que no sean de confianza, ya que pueden contener _malware_.
    - Algunos juegos tienen protecciones anti-trampas que pueden detectar o prevenir la inyección de código.
    - El código inyectado en un proceso puede acceder directamente a la memoria del proceso y modificarla sin necesidad de utilizar las funciones `ReadProcessMemory` o `WriteProcessMemory`.
    - Al inyectar una DLL, se debe asignar un nombre único para evitar conflictos con otras DLLs del sistema.
    - Es importante cerrar los _handles_ a los _threads_ creados para evitar problemas de memoria.
    - El uso de un _debugger_ puede ser útil para probar y depurar el código inyectado en un proceso.
    - Para evitar que la DLL inyectada se vea afectada por la protección ASLR (Address Space Layout Randomization) es recomendable desactivarla o usar técnicas para evitarla.
    - En algunos casos puede ser necesario usar funciones como `VirtualProtect` para poder escribir en regiones de memoria que son de solo lectura.
    - El código inyectado en un proceso también puede obtener la dirección base del módulo principal del proceso para acceder a sus datos usando técnicas de _assembly_.

## 6. Técnicas de Hooking

- **Concepto General**: El _hooking_ es una técnica que permite **interceptar y modificar el flujo de ejecución de un programa, redireccionando llamadas a funciones específicas a una función definida por el hacker**. Esto se logra mediante la modificación del código o las tablas de direcciones de funciones para que, en lugar de ejecutarse la función original, se ejecute primero el código del _hook_.
    
- **Propósito del Hooking**:
    
    - **Intercepción de Funciones:** El objetivo principal del _hooking_ es interceptar llamadas a funciones, ya sean de la API de Windows (WinAPI), de la API Direct3D, o funciones internas del propio juego.
    - **Modificación del Comportamiento:** Una vez interceptada la llamada a la función, se puede modificar su comportamiento, alterar los parámetros de entrada o salida, o incluso impedir su ejecución.
    - **Análisis y Monitoreo:** El _hooking_ también se utiliza para analizar el comportamiento de un programa, rastrear sus llamadas a funciones y obtener información sobre su funcionamiento.
    - **Implementación de Funcionalidades Adicionales:** En _game hacking_, el _hooking_ permite agregar funcionalidades nuevas a un juego, como _wallhacks_, _aimbots_, o _bots_.
- **Tipos de Hooking**:
    
    - **API Hooking**:
        
        - **Objetivo:** Interceptar llamadas a las funciones de la API de Windows, como `CreateProcess`, `LoadLibrary`, `ReadProcessMemory`, `WriteProcessMemory`, `TextOutA` o funciones de red como `send` y `recv`.
        - **Métodos**:
            - **IAT Hooking (Import Address Table)**: Se modifica la tabla de importación de un módulo para que las llamadas a las funciones de la API se dirijan al _hook_ en lugar de a la función original.
                - Es útil para interceptar llamadas a las API de Windows de forma específica por módulo.
            - **Inline Hooking**: Se modifica el código de la función original, generalmente al inicio de la función, insertando un salto (_jump_) a la función _hook_, que ejecutará el código deseado y luego puede ejecutar o no la función original.
                - Requiere modificar la memoria donde se encuentra la función, lo cual puede requerir el cambio de permisos de la misma con funciones como `VirtualProtect`.
                - A veces, los primeros bytes de la función original se copian en una función _trampoline_, que después de ejecutar el código original, devuelve el control a la función _hook_.
        - **Trampoline**: Un _trampoline_ es una función pequeña que guarda los registros, llama a la función original y restaura los registros. Se utiliza en inline hooking para asegurar que la función original se ejecute correctamente.
        - **Usos**:
            - Ocultar la presencia de malware.
            - Modificar el comportamiento de las funciones de la API.
            - Redirigir llamadas a otras funciones.
            - Interceptar llamadas a funciones de dibujado como `TextOutA` en un juego.
            - Monitorear el uso de las API por un programa.
    - **Direct3D Hooking**:
        
        - **Objetivo**: Interceptar y modificar las llamadas a las funciones de la API Direct3D, una API de gráficos utilizada por muchos juegos.
        - **Métodos**:
            - **VF Table Hooking (Virtual Function Table)**: Se modifica la tabla de funciones virtuales de un objeto Direct3D para que las llamadas a funciones específicas, como `EndScene()` o `Reset()`, se dirijan a la función _hook_.
            - **Jump Hooking**: Se inserta un salto al principio de una función de Direct3D para redireccionar la ejecución a la función _hook_, lo cual es útil cuando no se puede usar el _VF Table Hooking_.
        - **Usos**:
            - Crear _wallhacks_, que permiten ver a través de las paredes.
            - Modificar la iluminación del juego.
            - Añadir información adicional a la pantalla (HUDs).
            - Crear efectos gráficos personalizados.
    - **Kernel Mode Hooking**:
        
        - **Objetivo**: Interceptar llamadas a las funciones del núcleo del sistema operativo (kernel).
        - **Métodos**:
            - **SSDT Hooking (System Service Descriptor Table)**: Se modifica la tabla de descriptores de servicios del sistema para que las llamadas a las funciones del kernel se dirijan al _hook_.
                - Puede ser usado para ocultar la presencia de malware.
            - **Code Patching**: Se modifica el código de las funciones del kernel para redirigir la ejecución.
        - **Usos**:
            - Ocultar procesos, archivos o entradas de registro.
            - Interceptar llamadas a funciones de gestión de memoria o de acceso al sistema.
    - **Otras Técnicas**:
        
        - **Call Hooking**: Se modifica la dirección de destino de una instrucción CALL para que la ejecución se dirija a la función _hook_.
        - **Hooking de Mensajes de Teclado:** Se utiliza la función `SetWindowsHookEx` para interceptar los mensajes de teclado y registrar las pulsaciones de teclas.
        - **Hooking de Funciones de Paquetes de Red**: Para interceptar los datos enviados y recibidos por un juego, se pueden _hookear_ las funciones encargadas de procesar los paquetes de red.
- **Herramientas para Hooking:**
    
    - **API Monitor**: Herramienta para monitorear y analizar las llamadas a las API de Windows.
    - **Deviare API Hook**: Un motor de hooking para funciones de Win32 y objetos COM.
    - **Microsoft Detours**: Una biblioteca para _hooking_ de APIs de Win32, basada en _jump hooks_.
    - **MadCHook**: Otra biblioteca para _hooking_ que detecta y sigue otros _hooks_.
    - **GMER/Ring3 API Hook Scanner**: Herramientas para detectar _hooks_ en un sistema.
- **Implementación de un Hook**:
    
    1. **Identificar la función objetivo:** Determinar la función específica que se va a _hookear_.
    2. **Crear la función _hook_:** Desarrollar el código que se ejecutará cuando se intercepte la llamada a la función objetivo.
    3. **Modificar la función objetivo:** Insertar el _hook_ en la función objetivo, ya sea mediante IAT _hooking_ o _inline hooking_.
    4. **Llamar a la función original (opcional):** Dentro de la función _hook_, se puede decidir si se llama o no a la función original.
    5. **Gestionar el stack y los registros:** Asegurar que la función _hook_ gestione correctamente el _stack_ y preserve los registros para evitar errores en el programa.
    6. **Restaurar el estado original (en caso necesario):** En inline hooking, es necesario restaurar la función original después de que la función hook haya terminado su trabajo.
- **Consideraciones Importantes:**
    
    - El _hooking_ es una técnica poderosa que puede ser utilizada con fines maliciosos para crear _rootkits_ que ocultan la presencia de malware.
    - Es importante tener en cuenta que algunos juegos tienen protecciones _anti-cheat_ que pueden detectar y prevenir el uso de _hooks_.
    - Algunas funciones de la API de Windows tienen protecciones adicionales que hacen más difícil el _hooking_.
    - El _hooking_ puede generar problemas de estabilidad si no se implementa correctamente.
    - Para hacer _hooks_ en el kernel, se requieren permisos especiales y técnicas más avanzadas.

## 7. Desarrollo de Bots

- **Concepto General**: El desarrollo de bots implica la creación de programas que **automatizan acciones dentro de un juego**. Estos bots pueden variar desde simples asistentes hasta programas complejos capaces de jugar de forma autónoma. La clave para su desarrollo reside en la combinación de técnicas de manipulación de memoria, _hooking_, y simulación de entrada, junto con principios de teoría de control, máquinas de estado y algoritmos de búsqueda.
    
- **Componentes Clave en el Desarrollo de Bots**:
    
    - **Manipulación de Memoria**:
        - **Escaneo de memoria**: Los bots utilizan herramientas como Cheat Engine para **buscar direcciones de memoria donde se almacenan datos importantes** del juego, como la salud, la posición, el dinero, etc.
        - **Modificación de memoria**: Una vez encontradas estas direcciones, el bot puede **leer y escribir valores en la memoria** del juego para modificar el comportamiento del mismo. Por ejemplo, un bot podría modificar su salud o la cantidad de dinero que tiene.
        - **Punteros estáticos**: Los bots deben utilizar punteros estáticos que siempre apunten a la ubicación de memoria del jugador, porque las direcciones de memoria pueden cambiar cada vez que se reinicia el juego.
    - _**Hooking**_:
        - **Intercepción de funciones**: Los bots utilizan el _hooking_ para **interceptar llamadas a funciones** del juego o del sistema operativo. Esto les permite controlar el flujo de ejecución del juego y modificar su comportamiento.
        - **Modificación del comportamiento**: Al interceptar una función, el bot puede **alterar los parámetros, los resultados o el comportamiento de la misma**, lo que permite añadir nuevas funcionalidades o modificar las existentes. Por ejemplo, _hookear_ una función de dibujado puede ser útil para crear un _wallhack_.
    - **Simulación de Entrada (Teclado y Mouse)**:
        - **Emulación de acciones**: Los bots necesitan simular las acciones que un jugador humano realizaría, como presionar teclas o mover el mouse. Para ello, se utilizan funciones del sistema operativo, como `SendInput()` o `SendMessageA()`.
        - **Automatización de tareas**: Al simular estas acciones, el bot puede **automatizar tareas repetitivas** o reaccionar a eventos dentro del juego.
        - **Evitar detecciones**: Es importante usar todos los mensajes de teclado (WM_KEYDOWN, WM_CHAR, WM_KEYUP) para evitar que el bot sea detectado.
    - **Teoría de Control**:
        - **Retroalimentación**: Los bots deben implementar bucles de retroalimentación donde se utilizan sensores (lectura de memoria, _hooks_) para obtener el estado del juego, y un controlador para tomar decisiones y realizar acciones. Esto se basa en la teoría de control que permite a los bots actuar basándose en la información obtenida.
        - **Corrección de errores**: Los bots también pueden implementar mecanismos de corrección de errores para ajustarse a situaciones imprevistas y mejorar su comportamiento. Por ejemplo, un bot que sana podría ajustar su comportamiento si detecta que su curación no tuvo el efecto deseado.
    - **Máquinas de Estado**:
        - **Organización del comportamiento**: Las máquinas de estado permiten organizar el comportamiento de un bot en **diferentes estados**, donde cada estado representa una tarea específica. Por ejemplo, un bot podría tener un estado para buscar enemigos, otro para atacarlos y otro para recoger botín.
        - **Transición entre estados**: El bot **transiciona entre estados** en función de eventos del juego o decisiones tomadas por el controlador.
        - **Bots curadores**: Un bot curador puede tener un estado "salud baja" que lo hace tomar una poción y regresar a un estado de "salud normal".
        - **Flexibilidad**: Las máquinas de estado pueden ser modificadas y combinadas con la teoría del control para conseguir los resultados deseados.
    - **Algoritmos de Búsqueda**:
        - **Pathfinding**: Los bots necesitan algoritmos de búsqueda para encontrar caminos óptimos, por ejemplo, en mapas del juego. Un ejemplo sería el algoritmo A*.
        - **Selección de objetivos**: También se usan algoritmos de búsqueda para encontrar el enemigo más cercano o la ruta más corta para recolectar objetos.
        - **Optimización de acciones**: Los algoritmos de búsqueda ayudan a optimizar las acciones de los bots en la búsqueda de objetivos.
- **Lenguajes de programación:**
    
    - **C++:** Es un lenguaje muy utilizado para el desarrollo de bots debido a su capacidad para la manipulación de bajo nivel de memoria.
    - **Lua**: Es un lenguaje de alto nivel que se puede incrustar en programas C++ para la automatización de tareas. Es muy útil para añadir flexibilidad al bot.
- **Tipos de Bots**:
    
    - **Bots Reactivos**:
        - **Respuesta a eventos**: Estos bots **reaccionan a eventos** dentro del juego, como una disminución de la salud del jugador o la aparición de un enemigo.
        - **Ejemplos**: _Autohealers_ (bots que usan pociones automáticamente cuando la salud es baja), _autocombo_ (bots que hacen ataques combinados automáticamente).
        - **Técnicas**: Se utilizan _hooks_ para detectar eventos, modificaciones de memoria para obtener el estado del juego y simulación de entradas para realizar acciones.
    - **Bots Autónomos**:
        - **Automatización completa**: Estos bots **pueden jugar un juego completo sin intervención humana**.
        - **Ejemplos**: _Cavebots_ (bots que exploran cuevas y recolectan botín), _warbots_ (bots que combaten contra otros jugadores).
        - **Técnicas**: Usan la teoría de control, máquinas de estado y algoritmos de búsqueda para tomar decisiones y realizar acciones.
        - **Acciones**: Pueden curarse, recoger botín, caminar, vender objetos, comprar provisiones, etc.
    - **Clicker bots**: Son bots sencillos que ejecutan acciones repetitivas usando la simulación del teclado y el ratón. No interactúan directamente con la memoria del juego. Son fáciles de crear pero poco fiables.
- **Consideraciones Adicionales**:
    
    - **Detección de bots**: Los desarrolladores de juegos utilizan software anti-trampa para detectar bots, monitoreando comportamientos inusuales, como movimientos muy precisos o patrones repetitivos.
    - **Evasión de la detección**: Los desarrolladores de bots usan técnicas para evitar la detección, como la aleatorización de acciones o la simulación de movimientos humanos.
    - **Interacción con servidores**: Algunos bots pueden interactuar directamente con el servidor del juego, simulando ser un cliente de juego legítimo.
    - **Scripts**: Los bots deben tener la capacidad de ejecutar scripts para que los usuarios puedan añadir soporte para nuevas funcionalidades y personalizar su comportamiento.
- **Ejemplo Práctico (Bot de Curación)**: Un bot de curación podría funcionar de la siguiente manera:
    
    1. **Lectura de memoria**: El bot lee la dirección de memoria donde se almacena la salud del personaje.
    2. **Condición**: Si la salud es menor a un cierto valor (por ejemplo, 500), el bot ejecuta la siguiente acción.
    3. **Simulación de acción**: El bot simula presionar el botón de curación.
    4. **Repetición**: El bot repite este ciclo continuamente.
- **Herramientas para el Desarrollo de Bots**:
    
    - **Cheat Engine**: Para buscar y modificar direcciones de memoria.
    - **OllyDbg y x64dbg**: Para depurar y analizar el comportamiento del juego.
    - **Process Monitor**: Para monitorear las acciones de un proceso, como accesos a archivos, registros y al sistema.
    - **Visual Studio**: IDE para escribir código en C++.
    - **AutoIt y AutoHotKey**: Lenguajes de scripting para la automatización y la simulación de acciones.
    - **SDK de DirectX**: Para el _hooking_ de gráficos.

## 8. Evasión de Anti-Cheat

- **Concepto General**: Los sistemas anti-cheat son programas diseñados para **detectar y prevenir el uso de trampas (cheats) y bots en juegos**. Estos sistemas emplean una variedad de técnicas para identificar actividades sospechosas y, en consecuencia, tomar medidas como la expulsión del jugador (kick) o el bloqueo permanente de la cuenta (ban). La evasión del anti-cheat es un **juego constante de "gato y ratón"** donde los desarrolladores de bots buscan formas de eludir la detección, mientras que los desarrolladores de juegos mejoran sus sistemas anti-trampas.
    
- **Técnicas de Detección de Anti-Cheat**: Los sistemas anti-cheat emplean diversas técnicas, que se pueden clasificar en:
    
    - **Detección Basada en Firmas (SBD)**:
        - **Búsqueda de código específico**: Los sistemas anti-cheat **buscan fragmentos de código** o patrones binarios que se sabe que están asociados con bots o _cheats_. Es similar a como los antivirus buscan firmas de malware.
        - **Vulnerabilidad**: Esta técnica es vulnerable a la **ofuscación de código** y a la modificación de los binarios del bot.
    - **Verificación de la Integridad de Archivos**:
        - **Validación de archivos**: El anti-cheat **comprueba que los archivos del juego no han sido modificados** por los usuarios. Esto se logra mediante la generación de _hashes_ de los archivos y comparándolos con valores predefinidos.
        - **Evasión**: Para evadir esta técnica, se puede **modificar el archivo y cambiar el _hash_** correspondiente.
    - **Detección de Inyección de DLL**:
        - **Monitorización**: El anti-cheat **detecta cuando se inyectan bibliotecas de enlace dinámico (DLLs)** en el proceso del juego, una técnica común para introducir código de terceros.
        - **Engaño**: Los _hackers_ pueden intentar ocultar la inyección de DLL usando un "envoltorio" o _wrapper_.
        - **Uso legítimo**: Es importante notar que la inyección de DLLs no es necesariamente maliciosa. Se usa también por herramientas de accesibilidad o para depurar programas.
    - **Detección de _Hooks_**:
        - **Monitorización de llamadas**: El anti-cheat **detecta cuando se interceptan (_hook_) las llamadas a las funciones del sistema o del juego**. Los _hooks_ son una técnica muy usada para modificar el comportamiento de un programa.
        - **Evasión**: Se puede intentar evitar la detección de _hooks_ mediante el uso de **técnicas de ofuscación** o _hooking_ en niveles más bajos del sistema.
    - **Monitorización de Memoria**:
        - **Análisis de cambios**: El anti-cheat **analiza la memoria del juego en busca de cambios sospechosos** o patrones de acceso que indiquen el uso de un bot.
        - **Lectura y escritura**: El anti-cheat puede bloquear funciones de lectura y escritura de memoria.
        - **Evasión**: Se utilizan técnicas como la **ofuscación de datos** y la modificación de punteros para evadir esta detección.
        - **Spoofing de memoria**: Los _hackers_ pueden intentar engañar al sistema anti-cheat mediante _spoofing_ de memoria, aunque esto es más difícil si se realiza desde un _driver_ en modo kernel.
    - **Detección de Depuradores**:
        - **Búsqueda de depuradores**: El anti-cheat **detecta si hay un depurador** conectado al proceso del juego. Un depurador es una herramienta de programación que permite examinar la ejecución de un programa paso a paso.
        - **Evasión**: Se pueden usar técnicas anti-depuración para **ocultar la presencia de un depurador**.
    - **Detección de _Sandboxes_ y Máquinas Virtuales (VM)**:
        - **Identificación de entornos**: El anti-cheat intenta **identificar si el juego se está ejecutando en un entorno aislado** (como una _sandbox_ o una VM), ya que estos entornos son comunes para analizar el malware o ejecutar bots.
        - **Evasión**: Se utilizan técnicas anti-análisis para **evitar ser detectado en entornos virtuales**, ya que estos pueden ser usados por los desarrolladores de bots o por los analistas de malware..
    - **Análisis de Comportamiento**:
        - **Patrones sospechosos**: Los sistemas anti-cheat utilizan **inteligencia artificial y aprendizaje automático** para detectar patrones de comportamiento sospechosos que son característicos de los bots, como movimientos muy precisos, tiempos de respuesta extremadamente rápidos o la ejecución de secuencias repetitivas de acciones.
    - **Heurísticas**: El anti-cheat **analiza las características del programa en busca de patrones internos** que puedan indicar que es un bot. Asigna una puntuación a cada patrón, y si la puntuación total es mayor que un valor, considera el programa como un bot.
    - **Evasión**: Es importante que los bots **emulen el comportamiento humano** para evadir estos análisis.
    - **Captura de Pantalla**:
    - **Obtención de imágenes**: El anti-cheat puede **tomar capturas de pantalla** del juego para detectar visualmente el uso de trucos como _wallhacks_ o _aimbots_.
    - **Evasión**: Los bots pueden tratar de **evitar la captura de pantalla** o incluso alterarla.
    - **Análisis de Tráfico de Red**:
    - **Detección de patrones**: El anti-cheat puede **analizar los patrones de tráfico de red** para detectar actividades sospechosas que puedan indicar el uso de bots.
    - **Intercepción de paquetes**: El anti-cheat puede **detectar si se están interceptando los paquetes de red** para leer y manipular la información del juego.
    - **Cifrado**: Se usa cifrado para proteger el tráfico del juego y dificultar la creación de bots.
    - **Evasión**: Los bots pueden intentar **cifrar y manipular el tráfico de red** para ocultar sus acciones.
- **Monitoreo de Hardware**:
    
    - **Huella digital de hardware**: Los sistemas anti-cheat pueden **crear una "huella digital" del hardware** del jugador para detectar si la misma computadora se usa en varias cuentas, una señal común de uso de bots.
    - **Bloqueo de hardware**: Algunos sistemas como PunkBuster pueden llegar a bloquear permanentemente el acceso a un juego desde un determinado hardware.
- **Técnicas de Evasión de Anti-Cheat**: Los desarrolladores de bots utilizan diversas técnicas para evitar la detección, incluyendo:
    
    - **Ofuscación de Código**:
        - **Dificultar el análisis**: La ofuscación de código consiste en **hacer que el código del bot sea difícil de entender y analizar**.
        - **Técnicas**: Se usan técnicas como la codificación de _strings_, el uso de código basura, el cifrado y el _packing_ del ejecutable.
    - _**Packing**_:
        - **Compresión y cifrado**: El _packing_ **comprime y cifra el ejecutable del bot**, lo que dificulta su análisis. Al ejecutarse, el _packer_ descifra el código en la memoria para su ejecución.
        - **Herramientas**: Algunos _packers_ comunes son UPX, Armadillo, Themida y ASPack.
    - **Anti-Depuración**:
        - **Evasión de depuradores**: El bot implementa **técnicas para detectar y evitar la depuración** para dificultar el análisis de su código.
        - **Comportamiento alterado**: Cuando un depurador es detectado, el bot puede alterar su comportamiento, dificultando aún más el análisis.
    - **Uso de _Proxies_**:
    - **Redirección de tráfico**: Los bots usan _proxies_ para **redireccionar su tráfico de red**, ocultando así la dirección IP real del usuario y dificultando su identificación.
    - **Evitar bloqueos**: Los _proxies_ pueden ayudar a evitar el bloqueo de IP o la limitación de acceso.
    - **Manipulación de la Información del Juego**:
        - **Modificación de datos**: Los bots intentan **modificar la información que se envía al servidor del juego** para que parezca que las acciones son realizadas por un jugador legítimo.
        - **Emulación del jugador**: Los bots también deben tener la capacidad de emular las acciones de un jugador legítimo para evitar ser detectados por el análisis de comportamiento.
        - **Bypassing de funciones**: Si el anti-cheat interfiere con las funciones usadas para modificar la memoria, el bot debe copiar esas funciones a una nueva DLL y realizar las modificaciones en esta copia.
        - **Simulación de mensajes del teclado**: El bot debe usar todos los mensajes del teclado (WM_KEYDOWN, WM_CHAR, WM_KEYUP) para simular la entrada de manera efectiva y evitar la detección.
    - **Minimización de la Huella del Bot**:
    - **Ocultación**: Los bots deben **minimizar su huella** para evitar la detección, usando nombres de archivo y procesos genéricos, y ocultando su interfaz.
    - **Nombres aleatorios**: Usar nombres de archivo y directorios aleatorios para el bot puede ayudar a evitar detecciones basadas en nombres específicos.
    - **Randomización de Acciones**:
        - **Variación de patrones**: Los bots **aleatorizan sus acciones** para evitar patrones repetitivos que puedan indicar el uso de un bot.
        - **Simulación de comportamiento humano**: El objetivo es que el bot simule el comportamiento de un jugador real.
- **Evasión de Capturas de Pantalla:**
    
    - **Ocultamiento**: Ocultar información en pantalla mediante el uso de imágenes o dibujar los gráficos de la _cheat_ sobre la pantalla del juego.
    - **Alteración**: Los _hackers_ pueden intentar alterar las capturas de pantalla enviadas al anti-cheat para que no se vean las trampas.
- **Ingeniería inversa del anti-cheat**:
    
    - **Análisis del sistema**: Los desarrolladores de _cheats_ dedican tiempo al análisis del anti-cheat para entender cómo funciona y encontrar las vulnerabilidades que pueden usar para realizar _by-passes_.
- **Hacerse pasar por una herramienta legítima**: Algunos _hackers_ pueden intentar que su _cheat_ o _bot_ parezca una aplicación de _software_ legítima.
    
- **Ejemplo Práctico (Evasión de Detección Basada en Firmas)**:
    
    1. **Análisis de la Firma**: El desarrollador del bot analiza el código del bot y busca los fragmentos de código que son detectados por el anti-cheat.
    2. **Ofuscación**: El desarrollador ofusca el código, por ejemplo, modificando el orden de las instrucciones o cifrando partes del código.
    3. **Prueba**: El desarrollador prueba el bot para verificar que la ofuscación ha sido efectiva y que ya no es detectado por el anti-cheat.
- **Herramientas para la Evasión de Anti-Cheat**:
    
    - **Depuradores (OllyDbg, x64dbg)**: Para analizar el comportamiento del juego y del anti-cheat.
    - **Desensambladores (IDA Pro, Ghidra)**: Para examinar el código binario del juego y del anti-cheat.
    - _**Packers**_: Para comprimir y cifrar el ejecutable del bot (UPX, Armadillo, Themida, ASPack).
    - **Herramientas de _hooking_**: Para interceptar llamadas a funciones.
    - **Herramientas de ofuscación**: Para dificultar el análisis del código.

## 9. Otros Aspectos Importantes

- **Redes:** Es útil entender el modelo OSI para entender cómo funciona la comunicación en red, aunque no es necesario al inicio.
- **Estructuras de datos y algoritmos:** Es útil tener conocimientos básicos para organizar y manipular la información.
- **Practica:** El aprendizaje de estas habilidades requiere mucha práctica y experimentación.
- **Recursos en línea:** Hay muchos foros, sitios web, videos y libros que pueden ayudarte en tu aprendizaje. Algunas recomendaciones son:
    - **UnknownCheats:** Es un foro con mucha información y código de hacks.
    - **GitHub:** Tiene muchos proyectos de código abierto para estudiar.
    - **Libros:** "Game Hacking" de Nick Cano y "Reversing Secrets" de Eldad Eilam son buenas opciones.
    - **Sitios de aprendizaje de C++:** learncpp.com y los tutoriales de The Cherno y The New Boston en YouTube.
    - **Telegram:** Gamehacking CLS &Programación
    - **Guided Hacking:** Tiene una "biblia" del game hacking y cursos para principiantes. (Sin embargo su plataforma es de pago, la administración es tóxica y toda la información que necesitas está en google, por lo que no se recomienda esta plataforma)

## 10.Recomendaciones

- **Comienza con juegos simples sin anti-cheat** para practicar las técnicas básicas.
- **No te desanimes por los fracasos**, es un proceso de aprendizaje que requiere tiempo y perseverancia.
- **Participa en foros y comunidades** para aprender de otros y compartir tus conocimientos.
- **Siempre ten en cuenta las implicaciones legales y éticas** del game hacking.

---

> Acá adjunto recursos importantes que considero que nos ayudará en nuestro proceso de aprendizaje.


# Recursos de aprendizaje
## GitHub
- [The Ultimate Game Hacking Resource](https://github.com/dsasmblr/game-hacking/)
- [The Ultimate Online Game Hacking Resource](https://github.com/dsasmblr/hacking-online-games/)
- [Topic: Game Bot](https://github.com/topics/game-bot?l=python&o=desc&s=stars)
- [Gaming using Computer Vision](https://github.com/paulonteri/play-game-with-computer-vision#gaming-using-computer-vision)
- [GameHacking.gg](https://github.com/jhllc/Unity-Game#gamehackinggg)
- [CTF Game Challenges](https://github.com/mrT4ntr4/CTF-Game-Challenges#ctf-game-challenges)
- [Game Hacking Academy](https://gamehacking.academy/)

## YouTube
- [loab](https://www.youtube.com/@loabical/videos)
- [DeadOverflow](https://www.youtube.com/@deadoverflow/videos)
- [Low Level](https://www.youtube.com/@LowLevelTV/videos)
- [GynvaelEN](https://www.youtube.com/@GynvaelEN)
- [aXXo](https://www.youtube.com/@axxo1337)
- [Baseult Private](https://www.youtube.com/@baseultprivate9137)
- [Apxaey](https://www.youtube.com/@apxaey1459)
- [iwanMods](https://www.youtube.com/@iwanMods)
- [Dex](https://www.youtube.com/@DexTag)
- [Cyborg Elf](https://www.youtube.com/@CyborgElf/videos)
- [Hack In The Box Security Conference](https://www.youtube.com/@hitbsecconf/videos)
- [OWASP DevSlop](https://www.youtube.com/@OWASPDevSlop)
- [247CTF](https://www.youtube.com/@247CTF)
- [The Cyber Mentor](https://www.youtube.com/@TCMSecurityAcademy)
- [XorEAX MrGamer](https://www.youtube.com/@xoreaxmrgamer/videos)
- [The Gsm Work](https://www.youtube.com/@TheGsmWork/videos)
- [Alan Levy](https://www.youtube.com/@soy-elmago/videos)
- [John Hammond](https://www.youtube.com/@_JohnHammond)
- [WiseCereal](https://www.youtube.com/@WiseCereal/videos)
- [Game Jacker](https://www.youtube.com/@GameJacker/videos)
- [cazz](https://www.youtube.com/@cazz)
- [EddyoT&G](https://www.youtube.com/@EddyoTutos/videos)
- [LiveOverflow](https://www.youtube.com/@LiveOverflow/videos)
- [Classic Game Hacking](https://www.youtube.com/@ClassicGameHacking/videos)
- [swedz c#](https://www.youtube.com/@SwedishTwat/videos)
- [Intigriti](https://www.youtube.com/@intigriti)
- [Kian Brose](https://www.youtube.com/@KianBrose/videos)
- [Null](https://www.youtube.com/@null7953/videos)
- [Guided Hacking](https://www.youtube.com/@GuidedHacking)
- [Cheat The Game](https://www.youtube.com/@ChrisFayte)
- [Stephen Chapman](https://www.youtube.com/@StephenChapman/videos)
- [CursoReversing](https://www.youtube.com/@cursoreversing1952)



---

# Recursos indexados a NotebookLM

- [GAME HACKING 1 – ANTI CHEAT BYPASS](https://pt.linkedin.com/posts/joas-antonio-dos-santos_game-hacking-1-anti-cheat-bypass-activity-6977431747588206592-Jp7V)
- [Game Hacking: Developing Autonomous Bots for Online Games](https://www.amazon.com/-/es/Game-Hacking-Developing-Autonomous-Online/dp/1593276699/ref=sr_1_1?__mk_es_US=%C3%85M%C3%85%C5%BD%C3%95%C3%91&s=books&sr=1-1)
- [Practical Video Game Bots: Automating Game Processes using C++, Python, and AutoIt](https://www.amazon.com/-/es/Ilya-Shpigor-ebook/dp/B07GRM2G5Q/ref=sr_1_1?__mk_es_US=%C3%85M%C3%85%C5%BD%C3%95%C3%91&s=books&sr=1-1)
- [Ghidra Software Reverse-Engineering for Beginners: Master the art of debugging, from understanding code to mitigating threats](https://www.amazon.com/-/es/Ghidra-Software-Reverse-Engineering-Beginners-understanding/dp/B0DJGQ91R5/ref=sr_1_1?__mk_es_US=%C3%85M%C3%85%C5%BD%C3%95%C3%91&s=books&sr=1-1)
- [Malware and Reverse Engineering Complete Collection by Joas](https://elhacker.info/ebooks%20Joas/Malware%20and%20Reverse%20Engineering%20Complete%20Collection%20by%20Joas.pdf)
- [Malware Analysis and Detection Engineering: A Comprehensive Approach to Detect and Analyze Modern Malware](https://www.amazon.com/-/es/Malware-Analysis-Detection-Engineering-Comprehensive/dp/1484261925/ref=sr_1_1?__mk_es_US=%C3%85M%C3%85%C5%BD%C3%95%C3%91&s=books&sr=1-1)
- [Mastering Malware Analysis: A malware analyst's practical guide to combating malicious software, APT, cybercrime, and IoT attacks , Second Edition](https://www.packtpub.com/en-cy/product/mastering-malware-analysis-9781803240244)
- [Mastering Reverse Engineering: Re-engineer your ethical hacking skills](https://www.packtpub.com/en-cy/product/mastering-reverse-engineering-9781788835299)
- [HOW TO START GAME HACKING](https://www.youtube.com/watch?v=yW_ZxqVDLVE&list=TLGGu1ufcUE521AzMTAxMjAyNQ)
- [Game Hacking Explained in 8 Minutes (And How to Protect Your Games)](https://www.youtube.com/watch?v=uBxGUcsQf-w)
- [How to LEARN HACKING](https://www.youtube.com/watch?v=3_VfW6bDBdE)
- [Learn Reverse Engineering (for hacking games)](https://www.youtube.com/watch?v=0_Eif2qGK7I)
