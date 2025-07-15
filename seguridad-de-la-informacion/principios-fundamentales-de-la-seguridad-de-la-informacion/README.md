# Principios Fundamentales de la Seguridad de la Información

1. [la-triada-cia.md](la-triada-cia.md "mention")

### 2.0 El Marco de Soporte AAA: Gestión de Identidad y Acceso

Para implementar eficazmente la Tríada CIA, se utiliza el marco AAA: **Autenticación, Autorización y Trazabilidad (Accounting)**.

* **2.1 Autenticación (Authentication):** Es el proceso de **verificar la identidad** de un usuario, sistema o servicio. Responde a la pregunta: "¿Quién eres?".
* **2.2 Autorización (Authorization):** Una vez autenticada la identidad, la autorización es el proceso de **otorgar o denegar permisos** específicos a recursos. Responde a la pregunta: "¿Qué tienes permitido hacer?".
* **2.3 Trazabilidad (Accounting / Accountability):** Es el registro y seguimiento de las acciones realizadas por una identidad autenticada. Responde a la pregunta: "¿Qué hiciste?".
*   Ejemplo:

    Un empleado ingresa su nombre de usuario y contraseña, y luego un código de su aplicación móvil para acceder a la red corporativa (Autenticación). Una vez dentro, su perfil de usuario solo le permite acceder a las carpetas del departamento de Marketing, pero no a las de Finanzas (Autorización). Cada archivo que abre o modifica queda registrado en los logs del servidor con su nombre de usuario y la marca de tiempo (Trazabilidad).

### 3.0 Conceptos Extendidos de la Seguridad Moderna

Con la evolución del panorama digital, la Tríada CIA se ha ampliado para incluir otros principios cruciales.

#### 3.1 Privacidad (Privacy)

La privacidad es el derecho de un individuo a controlar cómo se recopila, utiliza, almacena y comparte su información personal (PII - Personally Identifiable Information). Está estrechamente relacionada con la confidencialidad, pero se enfoca en el aspecto del consentimiento y el control del titular de los datos, a menudo regulado por leyes como el GDPR o la CCPA.

#### 3.2 No Repudio (Non-repudiation)

El no repudio es la garantía de que un sujeto (usuario o sistema) no puede negar la autoría de una acción previamente realizada. Proporciona una prueba irrefutable del origen e integridad de los datos.

*   Ejemplo:

    Cuando una persona firma un contrato digital utilizando una firma electrónica basada en certificados, se crea una prueba criptográfica que la vincula inequívocamente a ese documento. Dicha persona no puede negar ("repudiar") haber firmado el contrato, ya que solo su clave privada única podría haber generado esa firma.

### 4.0 La Tríada Antagónica DAD: Los Objetivos del Adversario

En contraposición a los objetivos de la CIA, los actores maliciosos persiguen la Tríada DAD: **Divulgación, Alteración y Denegación**.

* **4.1 Divulgación (Disclosure):** Es la violación de la **confidencialidad**, donde información sensible es expuesta a partes no autorizadas.
  * _Ataques comunes:_ Exfiltración de datos mediante troyanos, ataques de phishing, robo físico de dispositivos.
* **4.2 Alteración (Alteration):** Es la violación de la **integridad**, donde los datos son modificados o corrompidos de forma no autorizada.
  * _Ataques comunes:_ Inyección SQL para modificar registros en una base de datos, defacement de sitios web, manipulación de transacciones financieras.
* **4.3 Denegación (Denial):** Es la violación de la **disponibilidad**, donde se impide el acceso legítimo a los recursos.
  * _Ataques comunes:_ Ataques de Denegación de Servicio (DoS) y Denegación de Servicio Distribuido (DDoS), ataques de ransomware que cifran datos críticos.

## Análisis del Marco de Ciberseguridad del NIST

### 1.0 NIST Cybersecurity Framework (CSF)

El Marco de Ciberseguridad desarrollado por el **Instituto Nacional de Estándares y Tecnología (NIST)** de Estados Unidos es un conjunto de directrices, estándares y mejores prácticas voluntarias para gestionar el riesgo de ciberseguridad. Su propósito es proporcionar un lenguaje común y una metodología estructurada que permita a las organizaciones, tanto del sector público como del privado, evaluar y mejorar su capacidad para prevenir, detectar y responder a ciberataques.

El núcleo de este marco se organiza en cinco funciones concurrentes y continuas que articulan el ciclo de vida de la gestión del riesgo de ciberseguridad a un alto nivel.

### 2.0 Las Cinco Funciones del Marco de Ciberseguridad

Las actividades de gestión de la ciberseguridad, según el NIST CSF, se clasifican en las siguientes cinco funciones fundamentales:

1. **Identificar (Identify)**
2. **Proteger (Protect)**
3. **Detectar (Detect)**
4. **Responder (Respond)**
5. **Recuperar (Recover)**

Estas funciones no deben ser vistas como pasos secuenciales, sino como pilares interconectados que operan simultáneamente para fortalecer la postura de seguridad de una organización.

#### 2.1 Identificar (Identify)

Esta función se centra en desarrollar una comprensión organizacional para gestionar el riesgo de ciberseguridad en los sistemas, activos, datos y capacidades. El objetivo es conocer a fondo el entorno operativo para priorizar los esfuerzos de protección.

* **Actividades Clave:**
  * **Gestión de Activos:** Inventariar y clasificar todos los activos físicos (servidores, estaciones de trabajo) y lógicos (software, datos).
  * **Análisis de Riesgos:** Evaluar las amenazas (actores maliciosos, fallos del sistema) y vulnerabilidades (software sin parches, configuraciones débiles) asociadas a los activos.
  * **Estrategia de Gestión de Riesgos:** Definir el apetito de riesgo de la organización y establecer las políticas y procedimientos para gobernar la seguridad.
*   Ejemplo:

    Una entidad financiera realiza un análisis de riesgo sobre su plataforma de banca en línea. Identifica que la base de datos de clientes es un activo crítico (Tier 1). La evaluación revela una vulnerabilidad en una librería de software de terceros y la amenaza de grupos de ransomware que explotan dicha falla. Con esta información, la organización puede priorizar la mitigación de este riesgo específico.

#### 2.2 Proteger (Protect)

Esta función consiste en el diseño e implementación de las salvaguardas y controles de seguridad adecuados para asegurar la entrega de servicios críticos. La función de _Proteger_ apoya la capacidad de limitar o contener el impacto de un posible evento de ciberseguridad.

* **Actividades Clave:**
  * **Control de Acceso:** Implementar mecanismos como el Principio de Mínimo Privilegio (PoLP) y la autenticación multifactor (MFA).
  * **Seguridad de Datos:** Proteger la confidencialidad, integridad y disponibilidad de la información mediante cifrado en reposo y en tránsito.
  * **Ciclo de Vida de Desarrollo Seguro (SDLC):** Integrar la seguridad en todas las fases del desarrollo, adquisición y desmantelamiento de activos de TI.
*   Ejemplo:

    Para proteger el activo crítico del ejemplo anterior (la base de datos de clientes), el equipo de TI implementa un Web Application Firewall (WAF) para filtrar tráfico malicioso, aplica el cifrado AES-256 a los datos almacenados y restringe el acceso a la base de datos únicamente a los administradores autorizados mediante credenciales con MFA.

#### 2.3 Detectar (Detect)

Esta función permite la identificación oportuna de eventos de ciberseguridad. Una detección eficaz y proactiva es crucial para iniciar una respuesta rápida y minimizar el impacto de un incidente.

* **Actividades Clave:**
  * **Monitorización Continua:** Vigilar activamente las redes, sistemas y activos para identificar actividades anómalas o maliciosas.
  * **Análisis de Eventos y Anomalías:** Utilizar sistemas de detección de intrusiones (IDS/IPS) y plataformas de gestión de eventos e información de seguridad (SIEM).
  * **Procesos de Detección:** Establecer procedimientos claros para analizar y escalar posibles incidentes.
*   Ejemplo:

    La organización utiliza un SIEM que correlaciona logs del WAF, del sistema operativo del servidor de base de datos y de los sistemas de autenticación. El SIEM genera una alerta de alta prioridad al detectar múltiples intentos de inicio de sesión fallidos desde una IP no reconocida, seguidos de un inicio de sesión exitoso, lo que indica un posible ataque de fuerza bruta exitoso o el uso de credenciales comprometidas.

#### 2.4 Responder (Respond)

Esta función se activa una vez que se ha detectado un incidente de seguridad. Incluye todas las acciones necesarias para contener el impacto del evento y erradicar la amenaza del entorno.

* **Actividades Clave:**
  * **Planificación de la Respuesta:** Tener un Plan de Respuesta a Incidentes (IRP) bien definido y probado.
  * **Análisis y Contención:** Investigar la naturaleza del incidente, su alcance y aislar los sistemas afectados para prevenir una mayor propagación.
  * **Erradicación y Comunicación:** Eliminar la causa raíz del incidente (ej. malware, cuenta comprometida) y comunicar el evento a las partes interesadas según el plan.
*   Ejemplo:

    Al recibir la alerta del SIEM, el Equipo de Respuesta a Incidentes (IRT) ejecuta el IRP. Primero, aíslan el servidor comprometido de la red (contención). Luego, realizan un análisis forense para determinar las acciones del atacante (análisis). Finalmente, eliminan el malware y revocan las credenciales comprometidas (erradicación).

#### 2.5 Recuperar (Recover)

Esta función se enfoca en restaurar las capacidades o servicios que fueron afectados durante un incidente de ciberseguridad. El objetivo es implementar planes de resiliencia para volver a la operación normal de manera oportuna y segura.

* **Actividades Clave:**
  * **Planificación de la Recuperación:** Desarrollar y mantener un Plan de Recuperación ante Desastres (DRP) y un Plan de Continuidad del Negocio (BCP).
  * **Restauración de Sistemas:** Restaurar los sistemas y datos a partir de copias de seguridad seguras e inmutables.
  * **Mejora Continua:** Incorporar las lecciones aprendidas del incidente para mejorar las funciones de Identificar, Proteger, Detectar y Responder.
*   Ejemplo:

    Después de erradicar la amenaza, el equipo de TI restaura la base de datos desde la última copia de seguridad íntegra y validada, tomada antes del compromiso. Se realiza una reunión post-incidente donde se decide mejorar la política de contraseñas y acelerar la implementación de parches de seguridad para evitar incidentes similares en el futuro.

## Gestión y Objetivos de los Controles de Seguridad

### 1.0 Definición de Controles y Contramedidas

En el ámbito de la ciberseguridad, es fundamental comprender la diferencia y el propósito de los controles y las contramedidas como elementos clave en la gestión del riesgo.

#### 1.1 Controles de Seguridad

Un **control de seguridad** es cualquier tipo de salvaguarda, mecanismo o procedimiento implementado de manera **proactiva** para mitigar el riesgo. Su función es reducir la probabilidad de que una amenaza explote una vulnerabilidad o disminuir el impacto resultante de dicha explotación.

* **Propósito:** Gestión general y preventiva del riesgo.
* **Alcance:** Amplio, diseñado para proteger contra una variedad de amenazas.
* **Ejemplos:**
  * **Técnicos:** Firewalls, software antivirus/antimalware, sistemas de detección de intrusiones (IDS).
  * **Administrativos:** Políticas de seguridad, programas de capacitación y concienciación, procedimientos de gestión de incidentes.
  * **Físicos:** Guardias de seguridad, cerraduras, cámaras de vigilancia (CCTV).

#### 1.2 Contramedidas

Una **contramedida** es un tipo de control altamente específico, implementado de manera **reactiva** para neutralizar una amenaza o vulnerabilidad particular que ha sido identificada, a menudo después de un incidente.

* **Propósito:** Neutralizar una amenaza específica.
* **Alcance:** Estrecho y dirigido. Son altamente efectivas para su objetivo puntual, pero menos eficientes para la seguridad general.
*   Ejemplo Práctico:

    Tras sufrir un ataque de phishing exitoso que explotó la confianza de los empleados en un formato de correo electrónico específico, una organización implementa una regla de filtrado de correo avanzada (la contramedida) que bloquea o pone en cuarentena automáticamente cualquier mensaje con esas características precisas.

### 2.0 Atributos y Criterios de Evaluación de Controles

Para que un control sea considerado robusto y adecuado, debe evaluarse según varios criterios clave:

* **Funcionalidad y Eficacia:** El control debe realizar la función para la que fue diseñado de manera fiable, consistente y oportuna.
* **Garantía (Assurance):** Es el nivel de confianza en que un control de seguridad es efectivo en su aplicación y no fallará bajo presión.
* **Análisis de Costo-Beneficio:** El beneficio de seguridad proporcionado por un control debe superar su costo de implementación, mantenimiento y operación. Si el costo de mitigar un riesgo es mayor que el impacto potencial del propio riesgo, una organización puede optar por la **aceptación del riesgo**.

### 3.0 Objetivos de Control y Defensa en Profundidad

#### 3.1 Objetivos de Control

Un **objetivo de control** es una declaración formal del resultado deseado que se pretende alcanzar mediante la implementación de uno o varios controles.

* **Ejemplo de Objetivo:** "Asegurar que solo el personal autorizado pueda acceder a los datos de clientes clasificados como confidenciales".
* **Controles para lograr el objetivo:** Implementación de control de acceso basado en roles (RBAC), autenticación multifactor (MFA) y cifrado de la base de datos.

#### 3.2 Estrategia de Defensa en Profundidad (Defense in Depth)

Este es un principio estratégico fundamental que consiste en implementar **múltiples capas de controles de seguridad**. El objetivo es que, si una capa es vulnerada por un atacante, las capas subsecuentes puedan impedir o retrasar el avance del ataque.

* **Propiedades Clave:**
  1. **Independencia:** Los controles deben ser independientes. Un fallo en una capa (ej. el firewall perimetral) no debe causar un **fallo en cascada** que anule las demás capas (ej. la segmentación de la red o los controles de acceso al servidor).
  2. **Diversidad:** Se deben utilizar controles variados, tanto en funcionalidad (ej. un firewall y un antivirus) como en proveedor. Depender de un único proveedor para todas las soluciones de seguridad crea un único punto de fallo (single point of failure).

***

### 4.0 Implementación mediante Líneas Base de Seguridad

Una **línea base de seguridad (security baseline)** es un conjunto estandarizado de controles que establece el nivel mínimo de seguridad para un sistema o entorno. Organizaciones como el **NIST** publican líneas base recomendadas.

#### 4.1 El Principio de Proporcionalidad

La robustez de los controles aplicados debe ser proporcional a la criticidad y sensibilidad del activo que protegen. No es rentable aplicar el mismo nivel de seguridad a un servidor web público que a una base de datos que contiene secretos comerciales.

#### 4.2 Proceso de Adaptación de una Línea Base

Las líneas base genéricas rara vez se ajustan perfectamente a una organización específica. Por ello, se deben modificar mediante el siguiente proceso:

* **Acotación (Scoping):** Eliminar controles de la línea base que no son aplicables al entorno. (Ej: quitar controles de seguridad para mainframes si la empresa no los utiliza).
* **Adaptación (Tailoring):** Personalizar o ajustar los controles recomendados para que se alineen con las políticas y el entorno tecnológico de la organización. (Ej: modificar el requisito de longitud de contraseña de 16 a 14 caracteres según la política interna).
* **Compensación (Compensating):** Sustituir un control recomendado por otro que ofrezca un nivel de seguridad similar pero que sea más factible o asequible para la organización.
* **Complementación (Supplementing):** Añadir nuevos controles que no estaban en la línea base original para hacer frente a riesgos específicos del entorno de la organización.

### 5.0 Ciclo de Vida de la Implementación de Controles

El proceso para desplegar una línea base de seguridad de forma efectiva es cíclico:

1. **Seleccionar** la línea base apropiada.
2. **Modificar** la línea base mediante acotación, adaptación, compensación y complementación.
3. **Publicar** la configuración finalizada para su revisión y aprobación.
4. **Implementar** los controles en el entorno de producción.
5. **Evaluar y Monitorear** continuamente el rendimiento de los controles para asegurar su eficacia y realizar ajustes si es necesario.

## Clasificación Funcional de los Controles de Seguridad

Los controles de seguridad se pueden clasificar según su función operativa dentro de una estrategia de defensa. Esta clasificación ayuda a las organizaciones a implementar un enfoque de seguridad por capas (Defensa en Profundidad), abordando el riesgo antes, durante y después de un incidente.

### 1.0 Controles Preventivos (Preventive Controls)

Estos controles están diseñados para **impedir activamente** que un incidente de seguridad ocurra. Su objetivo es eliminar o reducir la probabilidad de que una amenaza pueda explotar una vulnerabilidad.

* **Objetivo:** Prevenir el éxito de un ataque.
* **Ejemplos Prácticos:**
  * **Listas de Control de Acceso (ACLs):** Reglas en firewalls y routers que bloquean el tráfico no autorizado.
  * **Hardening de Sistemas:** Proceso de configuración segura de un sistema para reducir su superficie de ataque (ej. deshabilitar puertos y servicios innecesarios).
  * **Software Antimalware:** Escanea y bloquea la ejecución de código malicioso.
  * **Políticas y Procedimientos (SOPs):** Controles administrativos que dictan el comportamiento seguro de los usuarios.

### 2.0 Controles Detectivos (Detective Controls)

Estos controles están diseñados para **identificar, registrar y alertar** sobre actividades maliciosas o anómalas, ya sean intentos fallidos o intrusiones exitosas. No previenen el ataque, pero proporcionan la visibilidad necesaria para iniciar una respuesta.

* **Objetivo:** Descubrir un ataque en curso o uno que ya ha ocurrido.
* **Ejemplos Prácticos:**
  * **Logs y Auditorías:** Registros de eventos del sistema, aplicaciones y redes que pueden ser analizados en busca de actividad sospechosa.
  * **Sistemas de Detección de Intrusiones (IDS):** Sensores que monitorizan el tráfico de red en busca de patrones de ataque conocidos.
  * **Sistemas de Gestión de Información y Eventos de Seguridad (SIEM):** Correlacionan y analizan logs de múltiples fuentes para detectar incidentes.

### 3.0 Controles Correctivos (Corrective Controls)

Estos controles se activan **después de que un incidente ha ocurrido** para limitar el daño, remediar los sistemas afectados y restaurar las operaciones a un estado normal y seguro.

* **Objetivo:** Reducir el impacto de un incidente y recuperar los sistemas.
* **Ejemplos Prácticos:**
  * **Restauración desde Copias de Seguridad (Backups):** Recuperar datos y sistemas a un estado previo al incidente.
  * **Gestión de Parches:** Aplicar parches de seguridad a una vulnerabilidad que fue explotada.
  * **Planes de Respuesta a Incidentes (IRP):** Procedimientos que guían al equipo de seguridad en la erradicación de la amenaza y la recuperación del sistema.

### 4.0 Controles Físicos (Physical Controls)

Estos controles protegen el acceso físico a las instalaciones, la infraestructura y el hardware de una organización. Son la primera línea de defensa para prevenir el robo, daño o acceso no autorizado a los activos de TI.

* **Objetivo:** Proteger el entorno físico de la organización.
* **Ejemplos Prácticos:**
  * **Guardias de seguridad y perros guardianes.**
  * **Sistemas de videovigilancia (CCTV) y alarmas.**
  * **Cerraduras, torniquetes y control de acceso con tarjetas de identificación.**

### 5.0 Controles Disuasorios (Deterrent Controls)

Estos controles tienen un **efecto psicológico** sobre los potenciales atacantes, desmotivándolos de intentar una intrusión. Su eficacia radica en la percepción del riesgo o del esfuerzo requerido para el atacante.

* **Objetivo:** Desmotivar a un atacante para que no inicie un ataque.
* **Ejemplos Prácticos:**
  * **Señales de advertencia:** Carteles como "Propiedad Privada" o "Zona Videovigilada".
  * **Banners de inicio de sesión:** Mensajes que advierten sobre las sanciones legales por el acceso no autorizado a un sistema informático.

### 6.0 Controles Compensatorios (Compensating Controls)

Estos controles se implementan como una **alternativa** cuando un control primario recomendado no es factible o es demasiado costoso de aplicar. Deben proporcionar un nivel de protección equivalente o superior, aunque a través de una tecnología o metodología diferente.

* **Objetivo:** Cubrir una brecha de seguridad cuando el control principal no puede ser utilizado.
*   Ejemplo Práctico:

    Una organización utiliza un sistema industrial (SCADA) antiguo que no es compatible con software antimalware moderno (control primario). Como control compensatorio, aíslan el sistema en un segmento de red separado (microsegmentación) y monitorizan de forma intensiva todo el tráfico de red que entra y sale de dicho segmento.

## Estructura Organizacional de la Seguridad: Roles, Responsabilidades y Equipos Especializados

### 1.0 Competencias Fundamentales del Profesional de Seguridad

Los profesionales de la seguridad de la información deben poseer un conjunto de competencias multidisciplinarias para proteger eficazmente los activos de una organización. Estas responsabilidades abarcan desde la estrategia y la política hasta la implementación técnica y la respuesta a crisis.

Las competencias clave incluyen:

* **Gestión de Riesgos:** Participar en evaluaciones de riesgo para identificar, analizar y mitigar amenazas y vulnerabilidades.
* **Implementación de Controles:** Adquirir, instalar y configurar dispositivos de seguridad (ej. firewalls, proxies) y software de protección (ej. antimalware, EDR).
* **Gestión de Acceso:** Establecer y mantener estrictos controles de acceso a los datos y sistemas, revisando periódicamente los privilegios de usuario.
* **Monitorización y Auditoría:** Supervisar registros de auditoría (logs) para detectar actividades anómalas o no autorizadas.
* **Respuesta a Incidentes:** Ejecutar los procedimientos adecuados para contener, erradicar y recuperarse de incidentes de seguridad, así como documentar e informar sobre los mismos.
* **Continuidad del Negocio:** Crear y probar planes de Continuidad del Negocio (BCP) y de Recuperación ante Desastres (DRP).
* **Formación y Concienciación:** Desarrollar e impartir programas de formación en seguridad para todo el personal de la organización.

### 2.0 La Política de Seguridad de la Información (PSI)

La **Política de Seguridad de la Información (PSI)** es un documento marco de alto nivel, aprobado por la dirección, que establece formalmente el enfoque, los objetivos y las responsabilidades de la seguridad dentro de una organización. Sirve como base para el desarrollo de estándares, procedimientos y directrices más específicos.

* **Ejemplo Práctico:** Una PSI puede contener políticas subsidiarias como la **Política de Uso Aceptable (AUP)**, que dicta a los empleados qué pueden y qué no pueden hacer con los recursos de TI de la empresa. Por ejemplo, puede prohibir el uso de dispositivos USB personales para prevenir la introducción de malware o especificar que el acceso a sitios de redes sociales está bloqueado para minimizar la pérdida de productividad y los riesgos de seguridad.

### 3.0 Jerarquía de Roles y Responsabilidades

La asignación de responsabilidades de seguridad depende del tamaño y la estructura de la organización, pero generalmente sigue una jerarquía clara:

#### 3.1 Alta Dirección (CISO, CSO)

La responsabilidad estratégica y legal última recae en la alta dirección (propietarios, junta directiva). La gestión operativa es delegada a un líder ejecutivo, como el:

* **Director de Seguridad de la Información (CISO - Chief Information Security Officer):** Enfocado en la seguridad de los datos y sistemas de información.
* **Director de Seguridad (CSO - Chief Security Officer):** Rol más amplio que puede incluir seguridad física además de la ciberseguridad.

#### 3.2 Gerencia de Dominios

Los gerentes de diferentes unidades de negocio (ej. TIC, Contabilidad, Operaciones) son responsables de implementar y supervisar la seguridad dentro de sus respectivos dominios, asegurando el cumplimiento de la PSI.

#### 3.3 Personal Técnico y Especializado (ISSO)

Este grupo es responsable de la implementación, mantenimiento y monitorización diaria de los controles de seguridad. Un rol clave aquí es el:

* **Oficial de Seguridad de Sistemas de Información (ISSO - Information Systems Security Officer):** Profesional técnico encargado de asegurar un sistema de información específico.

#### 3.4 Personal No Técnico

Todos los empleados tienen la responsabilidad de comprender y cumplir con la política de seguridad. El factor humano es a menudo el eslabón más débil; el incumplimiento por parte de un solo empleado puede comprometer toda la infraestructura de seguridad, sin importar la robustez de los controles técnicos.

### 4.0 Equipos y Metodologías Operativas Especializadas

#### 4.1 Centro de Operaciones de Seguridad (SOC - Security Operations Center)

Un SOC es una instalación centralizada donde un equipo de profesionales de la seguridad monitoriza, analiza y protege los activos de información de una organización de forma continua (a menudo 24/7). Utilizan herramientas como los SIEM para correlacionar eventos y detectar posibles incidentes. Los SOC son comunes en grandes corporaciones, agencias gubernamentales y sectores críticos como el de la salud.

#### 4.2 DevSecOps: Integración de la Seguridad en el Desarrollo

**DevSecOps** (Desarrollo, Seguridad y Operaciones) es un cambio cultural y metodológico que integra la seguridad en cada fase del ciclo de vida del desarrollo de software (SDLC).

* **Principio Clave: "Desplazamiento a la Izquierda" (Shift Left):** En lugar de probar la seguridad al final del proceso, se automatizan las revisiones de seguridad desde las etapas más tempranas del desarrollo para identificar y corregir vulnerabilidades de forma más rápida y económica.

#### 4.3 Equipos de Respuesta a Incidentes (CIRT, CSIRT, CERT)

Cuando ocurre una brecha de seguridad, se activa un equipo especializado. Estos equipos actúan como el punto central de coordinación para gestionar el incidente.

* **CIRT (Cyber Incident Response Team)**
* **CSIRT (Computer Security Incident Response Team)**
* **CERT (Computer Emergency Response Team)**

Su función es contener la amenaza, realizar análisis forenses para entender el alcance y el vector del ataque, erradicar la presencia del atacante y coordinar la recuperación de los sistemas afectados.
