# Protocolos de Comunicación

Para que dos computadoras puedan intercambiar información, no basta con conectarlas físicamente. Necesitan hablar el mismo idioma. Aquí es donde entran en juego los protocolos.

Un **protocolo de comunicación** es un conjunto estructurado de reglas, estándares y procedimientos que rigen el intercambio de datos entre dispositivos dentro de una red. Estas normativas aseguran que la comunicación sea ordenada, coherente y comprensible, independientemente de si los dispositivos son de diferentes fabricantes, sistemas operativos o arquitecturas.

En términos simples, un protocolo actúa como un **idioma común** que permite que los dispositivos se comuniquen de forma eficiente, segura y sin errores.

### <mark style="color:yellow;">Funciones Fundamentales</mark>

Todo protocolo de red cumple una serie de roles esenciales para garantizar el éxito de la transmisión.

* **Direccionamiento:** Especifica cómo se identifica el origen y el destino de los datos (por ejemplo, mediante direcciones IP o MAC) para garantizar que el mensaje llegue correctamente al receptor adecuado.
* **Encapsulación:** Define cómo se empaquetan los datos en Unidades de Datos de Protocolo (PDU). Este proceso agrega información de control, como encabezados (headers) y colas (trailers), a los datos originales para su tránsito por la red.
* **Control de flujo y errores:** Establece mecanismos para verificar la integridad de los datos entregados y regula la velocidad de transmisión para evitar que un emisor rápido sature a un receptor lento.
* **Negociación de conexión:** En protocolos orientados a conexión (como TCP), se encarga de los procesos de establecimiento, mantenimiento y cierre formal de las sesiones de comunicación.

### <mark style="color:yellow;">Características Técnicas</mark>

El comportamiento de un protocolo se define por variables específicas que dictan cómo se maneja la información.

* **Formato del mensaje:** Define la sintaxis estricta de los mensajes intercambiados (qué bits corresponden al encabezado, cuáles a los datos y cuáles al cierre).
* **Tamaño del mensaje:** Determina la unidad máxima de transmisión (MTU). La cantidad de datos que puede viajar en un solo paquete depende del tipo de red y del medio físico.
* **Sincronización:** Controla la temporización del flujo de datos, gestionando la velocidad y el ritmo al que se transmiten los bits para que el receptor pueda interpretarlos.
* **Codificación:** Convierte los datos lógicos en señales físicas (pulsos eléctricos, ondas de radio o luz) aptas para el medio de transmisión.
* **Patrón de mensaje (Acuse de recibo):** Define la interactividad de la comunicación. Algunos protocolos requieren que el receptor confirme cada paquete recibido (ACK), mientras que otros permiten el envío continuo sin confirmación.

***

### <mark style="color:yellow;">Protocolos Clave</mark>

Para organizar la inmensa variedad de protocolos existentes, la industria utiliza modelos de referencia que dividen la comunicación en capas lógicas. El más utilizado es el Modelo OSI (Open Systems Interconnection).

A continuación, se presenta una clasificación de los protocolos estándar según la capa en la que operan y su función principal:

| **Capa OSI**           | **Protocolos Comunes**           | **Función Principal**                                                   |
| ---------------------- | -------------------------------- | ----------------------------------------------------------------------- |
| **7. Aplicación**      | HTTP, HTTPS, DNS, SMTP, FTP      | Interacción directa con el software del usuario (web, email, archivos). |
| **6. Presentación**    | SSL/TLS, JPEG, MP3               | Traduce, cifra y comprime los datos para la aplicación.                 |
| **5. Sesión**          | SIP, NetBIOS, RPC                | Gestiona el establecimiento y cierre de sesiones entre hosts.           |
| **4. Transporte**      | TCP, UDP                         | Garantiza la fiabilidad (TCP) o velocidad (UDP) de la entrega de datos. |
| **3. Red**             | IP (IPv4/IPv6), ICMP, BGP        | Determina la mejor ruta (enrutamiento) y el direccionamiento lógico.    |
| **2. Enlace de Datos** | Ethernet, Wi-Fi, PPP             | Controla el acceso al medio físico y el direccionamiento físico (MAC).  |
| **1. Física**          | DSL, Bluetooth, Señales de Fibra | Transmisión binaria pura a través de medios físicos o inalámbricos.     |
