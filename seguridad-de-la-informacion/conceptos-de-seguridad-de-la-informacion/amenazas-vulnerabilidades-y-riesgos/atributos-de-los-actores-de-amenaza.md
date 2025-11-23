# Atributos de los Actores de Amenaza

<p align="center">La evolución del panorama de las amenazas cibernéticas ha transformado la forma en que se deben analizar y mitigar los riesgos de seguridad. Tradicionalmente, la detección se basaba en firmas para identificar amenazas estáticas como virus o vulnerabilidades de software conocidas. Sin embargo, la sofisticación creciente de los actores de amenaza ha hecho que los métodos basados en firmas sean insuficientes. Es imperativo, por lo tanto, analizar la naturaleza moderna de las amenazas cibernéticas a través de sus atributos clave: ubicación, intención y capacidad</p>

### 1. Ubicación del Actor de Amenaza

La procedencia del ataque es un factor determinante en la evaluación de riesgos. Los actores de amenaza se clasifican en función de su relación con el sistema objetivo.

#### 1.1. Amenazas Externas

Una amenaza externa se refiere a un actor que carece de credenciales o acceso autorizado al sistema objetivo. Para lograr la intrusión, estos actores comúnmente emplean tácticas como:

* Malware: Software malicioso diseñado para infiltrarse o dañar sistemas informáticos, como ransomware, spyware o troyanos.
* Ingeniería social: Manipulación psicológica para engañar a usuarios y obtener información confidencial o acceso, por ejemplo, a través de ataques de phishing o pretexting.

Ejemplo Práctico: Un grupo de ciberdelincuentes que, desde fuera de la red corporativa, intenta acceder a una base de datos mediante un ataque de fuerza bruta o explotando una vulnerabilidad no parcheada en un servidor web expuesto.

#### 1.2. Amenazas Internas (Insider Threats)

Una amenaza interna o amenaza de infiltrado involucra a individuos que poseen permisos legítimos dentro del sistema. Estos actores suelen ser:

* Empleados actuales o antiguos: Con acceso a información o sistemas sensibles.
* Contratistas o terceros: Con privilegios de acceso concedidos para realizar sus funciones.

La peligrosidad de una amenaza interna radica en su conocimiento del funcionamiento interno de la organización y el acceso preexistente.

Ejemplo Práctico: Un empleado descontento que, utilizando sus credenciales de acceso válidas, copia información confidencial de la empresa antes de renunciar, o un administrador de sistemas que introduce una puerta trasera para acceso futuro.

### 2. Intención y Motivación

Comprender la intención y motivación detrás de un ataque es crucial para predecir el comportamiento del adversario y desarrollar estrategias de defensa adecuadas.

#### 2.1. Intención

La intención define el objetivo final del atacante. Es el resultado que el actor de amenaza espera lograr mediante la ejecución del ataque.

Ejemplo: La intención puede ser el robo de datos, la interrupción de servicios, la modificación de información o el daño a la reputación.

#### 2.2. Motivación

La motivación es la razón subyacente que impulsa al actor a perpetrar el ataque. A menudo, la motivación se clasifica en las siguientes categorías:

* Lucro/Codicia: Obtención de beneficios económicos, como en el caso de ransomware o robo de información financiera.
* Curiosidad: Exploración de sistemas por desafío intelectual o descubrimiento de vulnerabilidades sin intención maliciosa inicial.
* Agravio/Venganza: Actos impulsados por resentimiento personal o profesional, común en empleados descontentos o antiguos colaboradores.
* Ideología/Activismo Social (Hacktivismo): Ataques realizados para promover una causa política o social, buscando generar conciencia o desestabilizar organizaciones.

#### 2.3. Estructura de la Amenaza

Las amenazas también pueden clasificarse por su nivel de organización y planificación:

*   Amenazas Estructuradas: Caracterizadas por una planificación meticulosa, coordinación y objetivos específicos. Estos ataques suelen ser perpetrados por grupos organizados, como bandas de ciberdelincuentes o actores patrocinados por estados-nación. Poseen un conocimiento profundo del objetivo y sus vulnerabilidades.

    Ejemplo Práctico: Un Grupo de Amenaza Persistente Avanzada (APT) que realiza una campaña de espionaje industrial, investigando exhaustivamente la infraestructura de la víctima, desarrollando exploits personalizados y manteniendo una presencia sigilosa a largo plazo para exfiltrar datos.
*   Amenazas No Estructuradas: Son ataques oportunistas y a menudo carecen de un plan detallado o un objetivo particular. Suelen ser ejecutados por individuos con habilidades técnicas limitadas, como los "script kiddies".

    Ejemplo Práctico: Un "script kiddie" que utiliza herramientas automatizadas disponibles públicamente para lanzar una campaña de spam masivo o intentar ataques de denegación de servicio (DoS) básicos contra sitios web aleatorios.

### 3. Capacidad y Sofisticación

El nivel de sofisticación y la capacidad de un actor de amenaza son indicadores clave de su potencial destructivo y la dificultad para detectarlo y neutralizarlo. Estos atributos están directamente relacionados con las habilidades técnicas y los recursos financieros disponibles para el adversario.

#### 3.1. Nivel de Habilidad Técnica

* Actores de Baja Capacidad (Ej. Script Kiddies): Dependen de herramientas de ataque preexistentes y scripts automatizados disponibles en la comunidad. Sus ataques son generalmente menos complejos y más fáciles de detectar.
* Actores de Alta Capacidad (Ej. Grupos APT, Cibercriminales Avanzados): Poseen la habilidad para desarrollar sus propios exploits, malware personalizado y técnicas de evasión avanzadas. Son capaces de identificar y explotar vulnerabilidades de día cero (zero-day exploits) en sistemas operativos y aplicaciones, que son desconocidas para los desarrolladores y las soluciones de seguridad.

#### 3.2. Recursos Financieros

La financiación es un factor crítico que determina la capacidad de un actor de amenaza:

* Grupos con Financiación Limitada: A menudo recurren a herramientas gratuitas o de bajo costo y sus operaciones pueden ser menos persistentes.
* Grupos con Financiación Significativa: Incluyen sindicatos criminales y actores patrocinados por estados-nación. Esta financiación les permite invertir en investigación y desarrollo (I+D) para descubrir nuevas vulnerabilidades, adquirir herramientas de ataque sofisticadas, contratar a expertos en seguridad ofensiva y mantener operaciones a gran escala durante períodos prolongados.

Ejemplo: Un grupo de ciberespionaje patrocinado por un estado-nación que desarrolla un exploit de día cero para un sistema operativo ampliamente utilizado, lo que les permite infiltrarse en redes gubernamentales y corporativas de alto valor sin ser detectados por las defensas tradicionales.

La comprensión profunda de estos atributos permite a las organizaciones desarrollar estrategias de ciberseguridad proactivas y más resilientes, pasando de una defensa reactiva basada en firmas a un enfoque adaptativo que anticipa las tácticas, técnicas y procedimientos (TTPs) de los adversarios modernos.
