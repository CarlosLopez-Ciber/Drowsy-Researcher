# Marco de Ciberseguridad del NIST

## NIST Cybersecurity Framework (CSF)

El Marco de Ciberseguridad desarrollado por el **Instituto Nacional de Estándares y Tecnología (NIST)** de Estados Unidos es un conjunto de directrices, estándares y mejores prácticas voluntarias para gestionar el riesgo de ciberseguridad. Su propósito es proporcionar un lenguaje común y una metodología estructurada que permita a las organizaciones, tanto del sector público como del privado, evaluar y mejorar su capacidad para prevenir, detectar y responder a ciberataques.

El núcleo de este marco se organiza en cinco funciones concurrentes y continuas que articulan el ciclo de vida de la gestión del riesgo de ciberseguridad a un alto nivel.

### Las Cinco Funciones del Marco de Ciberseguridad

Las actividades de gestión de la ciberseguridad, según el NIST CSF, se clasifican en las siguientes cinco funciones fundamentales:

1. **Identificar (Identify)**
2. **Proteger (Protect)**
3. **Detectar (Detect)**
4. **Responder (Respond)**
5. **Recuperar (Recover)**

Estas funciones no deben ser vistas como pasos secuenciales, sino como pilares interconectados que operan simultáneamente para fortalecer la postura de seguridad de una organización.

#### 1. Identificar (Identify)

Esta función se centra en desarrollar una comprensión organizacional para gestionar el riesgo de ciberseguridad en los sistemas, activos, datos y capacidades. El objetivo es conocer a fondo el entorno operativo para priorizar los esfuerzos de protección.

* **Actividades Clave:**
  * **Gestión de Activos:** Inventariar y clasificar todos los activos físicos (servidores, estaciones de trabajo) y lógicos (software, datos).
  * **Análisis de Riesgos:** Evaluar las amenazas (actores maliciosos, fallos del sistema) y vulnerabilidades (software sin parches, configuraciones débiles) asociadas a los activos.
  * **Estrategia de Gestión de Riesgos:** Definir el apetito de riesgo de la organización y establecer las políticas y procedimientos para gobernar la seguridad.
*   Ejemplo:

    Una entidad financiera realiza un análisis de riesgo sobre su plataforma de banca en línea. Identifica que la base de datos de clientes es un activo crítico (Tier 1). La evaluación revela una vulnerabilidad en una librería de software de terceros y la amenaza de grupos de ransomware que explotan dicha falla. Con esta información, la organización puede priorizar la mitigación de este riesgo específico.

#### 2. Proteger (Protect)

Esta función consiste en el diseño e implementación de las salvaguardas y controles de seguridad adecuados para asegurar la entrega de servicios críticos. La función de _Proteger_ apoya la capacidad de limitar o contener el impacto de un posible evento de ciberseguridad.

* **Actividades Clave:**
  * **Control de Acceso:** Implementar mecanismos como el Principio de Mínimo Privilegio (PoLP) y la autenticación multifactor (MFA).
  * **Seguridad de Datos:** Proteger la confidencialidad, integridad y disponibilidad de la información mediante cifrado en reposo y en tránsito.
  * **Ciclo de Vida de Desarrollo Seguro (SDLC):** Integrar la seguridad en todas las fases del desarrollo, adquisición y desmantelamiento de activos de TI.
*   Ejemplo:

    Para proteger el activo crítico del ejemplo anterior (la base de datos de clientes), el equipo de TI implementa un Web Application Firewall (WAF) para filtrar tráfico malicioso, aplica el cifrado AES-256 a los datos almacenados y restringe el acceso a la base de datos únicamente a los administradores autorizados mediante credenciales con MFA.

#### 3. Detectar (Detect)

Esta función permite la identificación oportuna de eventos de ciberseguridad. Una detección eficaz y proactiva es crucial para iniciar una respuesta rápida y minimizar el impacto de un incidente.

* **Actividades Clave:**
  * **Monitorización Continua:** Vigilar activamente las redes, sistemas y activos para identificar actividades anómalas o maliciosas.
  * **Análisis de Eventos y Anomalías:** Utilizar sistemas de detección de intrusiones (IDS/IPS) y plataformas de gestión de eventos e información de seguridad (SIEM).
  * **Procesos de Detección:** Establecer procedimientos claros para analizar y escalar posibles incidentes.
*   Ejemplo:

    La organización utiliza un SIEM que correlaciona logs del WAF, del sistema operativo del servidor de base de datos y de los sistemas de autenticación. El SIEM genera una alerta de alta prioridad al detectar múltiples intentos de inicio de sesión fallidos desde una IP no reconocida, seguidos de un inicio de sesión exitoso, lo que indica un posible ataque de fuerza bruta exitoso o el uso de credenciales comprometidas.

#### 4. Responder (Respond)

Esta función se activa una vez que se ha detectado un incidente de seguridad. Incluye todas las acciones necesarias para contener el impacto del evento y erradicar la amenaza del entorno.

* **Actividades Clave:**
  * **Planificación de la Respuesta:** Tener un Plan de Respuesta a Incidentes (IRP) bien definido y probado.
  * **Análisis y Contención:** Investigar la naturaleza del incidente, su alcance y aislar los sistemas afectados para prevenir una mayor propagación.
  * **Erradicación y Comunicación:** Eliminar la causa raíz del incidente (ej. malware, cuenta comprometida) y comunicar el evento a las partes interesadas según el plan.
*   Ejemplo:

    Al recibir la alerta del SIEM, el Equipo de Respuesta a Incidentes (IRT) ejecuta el IRP. Primero, aíslan el servidor comprometido de la red (contención). Luego, realizan un análisis forense para determinar las acciones del atacante (análisis). Finalmente, eliminan el malware y revocan las credenciales comprometidas (erradicación).

#### 5. Recuperar (Recover)

Esta función se enfoca en restaurar las capacidades o servicios que fueron afectados durante un incidente de ciberseguridad. El objetivo es implementar planes de resiliencia para volver a la operación normal de manera oportuna y segura.

* **Actividades Clave:**
  * **Planificación de la Recuperación:** Desarrollar y mantener un Plan de Recuperación ante Desastres (DRP) y un Plan de Continuidad del Negocio (BCP).
  * **Restauración de Sistemas:** Restaurar los sistemas y datos a partir de copias de seguridad seguras e inmutables.
  * **Mejora Continua:** Incorporar las lecciones aprendidas del incidente para mejorar las funciones de Identificar, Proteger, Detectar y Responder.
*   Ejemplo:

    Después de erradicar la amenaza, el equipo de TI restaura la base de datos desde la última copia de seguridad íntegra y validada, tomada antes del compromiso. Se realiza una reunión post-incidente donde se decide mejorar la política de contraseñas y acelerar la implementación de parches de seguridad para evitar incidentes similares en el futuro.
