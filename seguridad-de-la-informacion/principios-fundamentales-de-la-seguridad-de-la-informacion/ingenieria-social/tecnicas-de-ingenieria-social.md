# Técnicas de Ingeniería Social

## 1. Phishing

El **phishing** es, posiblemente, la técnica de ingeniería social más extendida. Su fundamento radica en **crear una sensación de emoción o pánico** en el objetivo, manipulando sus emociones a través de comunicaciones fraudulentas, predominantemente por correo electrónico.

* **Mecanismo:** Los atacantes envían correos electrónicos que simulan ser de entidades legítimas y confiables (bancos, proveedores de servicios, redes sociales, etc.). Estos correos suelen contener:
  * **Enlaces maliciosos:** Redirigen a sitios web falsos que imitan a los legítimos para capturar credenciales u otra información sensible.
  * **Archivos adjuntos infectados:** Contienen malware (ej. troyanos, ransomware) que se descarga e instala al ser abiertos.
* **Emociones Explotadas:** La urgencia, el miedo (amenazas de suspensión de cuenta, problemas de seguridad) o la excitación (ofertas, premios inesperados).

**Ejemplo Práctico:**

1. Un usuario recibe un correo electrónico que parece provenir de YouTube, alertando sobre "problemas con su cuenta" y proporcionando un enlace para "solucionarlos". Al hacer clic, el usuario es dirigido a una página falsa de inicio de sesión de YouTube diseñada para robar sus credenciales.
2. Otro ejemplo común es un correo que simula ser de PayPal, indicando un "problema con un depósito" y solicitando al usuario que "revise su cuenta" a través de un enlace fraudulento.

### 1.1. Spear Phishing (Phishing Dirigido)

El **spear phishing** es una variante del phishing caracterizada por su **alto nivel de especificidad y personalización**.

* **Objetivo:** Se dirige a un **individuo o una organización muy específicos**, no a una audiencia masiva. Los atacantes invierten tiempo en investigar a su objetivo para que el mensaje sea altamente relevante y convincente.
* **Sofisticación:** La personalización va más allá de usar el nombre del objetivo; puede incluir detalles sobre su trabajo, colegas, proyectos o intereses, haciendo el ataque extremadamente difícil de detectar.

**Ejemplo :** Un ingeniero de una empresa recibe un correo electrónico que parece ser de un colega de otro departamento, mencionando un proyecto en el que ambos están trabajando y solicitando revisar un "documento compartido" adjunto. El documento, en realidad, contiene un **malware** diseñado para obtener acceso a la red de la empresa.

### 1.2. Angler Phishing (Phishing de Pescador)

El **angler phishing** es una forma de phishing que se dirige específicamente a **usuarios de redes sociales**.

* **Mecanismo:** Los atacantes se hacen pasar por marcas, empresas o servicios al cliente en plataformas de redes sociales. Responden a quejas públicas o consultas de usuarios con mensajes maliciosos que contienen enlaces a sitios web de phishing o solicitan información personal a través de mensajes directos.
* **Contexto:** Aprovechan la necesidad de los usuarios de redes sociales de resolver problemas rápidamente o interactuar con el soporte de una empresa.

**Ejemplo :** Un cliente se queja en Twitter sobre un problema con su aerolínea. Un atacante, haciéndose pasar por la cuenta oficial de soporte de la aerolínea, le responde públicamente pidiéndole que envíe un mensaje directo con sus "detalles de reserva y contraseña para verificación". El enlace proporcionado en el mensaje directo lleva a un sitio web falso.

### 1.3. Whaling (Caza de Ballenas)

El **whaling** es una forma de phishing altamente dirigida a las **altas esferas ejecutivas** de una organización.

* **Objetivo:** Se dirige a "peces gordos" o **altos ejecutivos** (CEO, CFO, directores), dada su posición estratégica y acceso a información crítica o fondos.
* **Mecanismo:** Los mensajes son extremadamente sofisticados y convincentes, a menudo relacionados con fusiones y adquisiciones, auditorías o problemas legales, temas que solo serían relevantes para la alta dirección.
* **Impacto:** El éxito de un ataque de whaling puede tener consecuencias devastadoras para la organización.

**Ejemplo :** El CFO de una empresa recibe un correo electrónico que parece provenir del CEO, solicitando una transferencia urgente de fondos a una cuenta bancaria específica para una "adquisición confidencial" o una "auditoría interna inesperada".

## 2. Vishing (Phishing por Voz)

El **vishing** utiliza **llamadas telefónicas** para crear una sensación de urgencia, miedo o emoción, similar al phishing por correo electrónico.

* **Mecanismo:** Los atacantes se hacen pasar por representantes de instituciones de confianza (bancos, soporte técnico, agencias gubernamentales) para engañar a la víctima.
* **Tácticas Comunes:**
  * **Falsa Alerta de Seguridad:** Notifican a la víctima sobre supuestos virus en su computadora o actividad sospechosa en su cuenta.
  * **Soporte Técnico Fraudulento:** Se hacen pasar por personal de soporte de empresas como Microsoft, ofreciendo "ayuda" para "limpiar" el sistema.
  * **Ofertas Promocionales Engañosas:** Prometen descuentos o extensiones de garantías que requieren información personal o financiera.

**Ejemplo :** Un usuario recibe una llamada de alguien que se identifica como "Dick Jones de Microsoft", advirtiéndole que su computadora está infectada con virus y ofreciéndose a "ayudarlo" a solucionarlo. Para ello, le piden acceso remoto a su equipo o sus credenciales bancarias para un "servicio de pago".

## 3. Bulos (Hoaxes)

Los **bulos** son mensajes que difunden **información falsa** con el objetivo de causar alarma, confusión o pánico, aunque a menudo no son tan directamente maliciosos en su impacto técnico como el phishing.

* **Mecanismo:** El atacante puede hacerse pasar por un empleado descontento, un cliente enfadado, o incluso una autoridad para propagar rumores o advertencias falsas sobre virus, peligros inminentes o amenazas inexistentes.
* **Impacto:** Pueden generar una sobrecarga de trabajo para los equipos de TI y seguridad, desviar recursos y crear desconfianza interna.

**Ejemplo :** Un correo electrónico interno se difunde alertando sobre un "nuevo virus extremadamente peligroso" que borra todos los archivos si no se reenvía el correo a todos los contactos, o un mensaje en redes sociales que advierte sobre un "nuevo tipo de ataque que roba contraseñas solo con visitar una página".

## 4. Smishing (Phishing por SMS)

El **smishing** combina la inmediatez del mensaje de texto con las tácticas de ingeniería social para generar una **sensación de emoción o pánico** en el objetivo.

* **Mecanismo:** Se envían mensajes de texto (SMS) que contienen enlaces maliciosos o números de teléfono a los que se debe llamar para "resolver un problema urgente" o "reclamar un premio".
* **Contexto:** Los usuarios de teléfonos móviles son particularmente vulnerables debido a la confianza implícita en los SMS y la facilidad de hacer clic en enlaces desde un dispositivo móvil.

**Ejemplo Práctico:** Un usuario recibe un mensaje de texto que dice "Su entrega ha sido reprogramada. Haga clic en el enlace para confirmar" o "Felicidades, ha ganado un sorteo. Visite \[enlace malicioso] para reclamar su premio".

## 5. Estafa de la Factura (Business Email Compromise - BEC)

La **estafa de la factura**, a menudo el paso siguiente a un exitoso ataque de **whaling**, es una forma de fraude de suplantación de identidad dirigida a empresas.

* **Mecanismo:** Una vez que la cuenta de correo electrónico de un ejecutivo de alto nivel (CEO, CFO) ha sido comprometida mediante whaling, el atacante utiliza esa cuenta para enviar **facturas falsas o instrucciones de transferencia de fondos** al departamento de finanzas o a un empleado con autoridad para realizar pagos.
* **Objetivo Final:** Desviar grandes sumas de dinero a cuentas bancarias controladas por los atacantes.
* **Credibilidad:** La solicitud parece legítima porque proviene de una dirección de correo electrónico interna y de una persona con autoridad dentro de la empresa.

**Ejemplo :** Un atacante, habiendo comprometido la cuenta del Director de Operaciones (COO), envía un correo electrónico a la secretaria de finanzas con una factura por un servicio no realizado, solicitando un pago urgente a una cuenta bancaria externa que pertenece al atacante.

## 6. Baiting (Cebado)

El **baiting** es una táctica de ingeniería social que se basa en la **curiosidad o la codicia** de la víctima para que interactúe con un dispositivo o archivo malicioso.

* **Mecanismo:** El ejemplo clásico es dejar **unidades USB infectadas** en lugares públicos (ej. estacionamientos de empresas, cafeterías). El atacante espera que un empleado ingenuo recoja la unidad, la lleve al lugar de trabajo y la conecte a una estación de trabajo, infectando así su ordenador y potencialmente toda la red corporativa.
* **Disfraces:** Las unidades USB a menudo tienen etiquetas atractivas como "Confidencial" o "Nóminas".

**Ejemplo :** Un técnico de una empresa de seguridad encuentra una memoria USB sin etiquetar en el estacionamiento. Por curiosidad, la conecta a su laptop de trabajo. La unidad contiene un **ransomware** que encripta los datos del equipo y se propaga a otros sistemas de la red.

## 7. Ataque a la Hora de la Comida (Lunchtime Attack)

El "ataque a la hora de la comida" es una técnica de ingeniería social que aprovecha la **negligencia momentánea de los empleados** para obtener acceso no autorizado a sus estaciones de trabajo.

* **Mecanismo:** Se produce cuando un empleado se ausenta de su escritorio (ej. para ir a almorzar) sin bloquear o cerrar la sesión de su ordenador. Un atacante, a menudo una amenaza interna o alguien que ha obtenido acceso físico al área, aprovecha esta oportunidad.
* **Explotación:** El atacante puede sentarse en la estación de trabajo desatendida y acceder a archivos, aplicaciones o sistemas con los permisos del usuario legítimo.
* **Riesgo:** Permite el robo de datos, la instalación de malware o la manipulación de información sin dejar rastro de una intrusión técnica.

**Ejemplo :** Un empleado se levanta para almorzar dejando su sesión de Windows abierta. Un colega descontento o un intruso (que ya ha accedido al edificio) se acerca al escritorio y descarga documentos sensibles o instala un **keylogger** en el sistema del empleado.

## 8. Piggybacking (Acompañamiento)

El **piggybacking** es una técnica donde un atacante obtiene acceso a un área restringida **con el permiso explícito o implícito de un empleado autorizado**.

* **Mecanismo:** El atacante se presenta de una manera que persuade al empleado a abrirle una puerta de acceso seguro. Esto a menudo implica:
  * **Simular una situación de inconveniencia:** Cargar cajas pesadas para parecer incapaz de abrir la puerta.
  * **Generar un sentido de urgencia o camaradería:** Apelar a la empatía del empleado para que le "eche una mano" o que le permita el paso rápidamente.
  * **Engaño:** A veces, el atacante puede incluso fingir haber olvidado su tarjeta de acceso o estar teniendo problemas con ella.
* **Distinción Clave:** A diferencia del _tailgating_, en el _piggybacking_ hay una **interacción directa** con el empleado autorizado, quien voluntariamente permite el paso al atacante.

**Ejemplo :** En una escena de la película "Hackers", el protagonista (Robert Redford) se muestra cargando voluminosas cajas de globos en la entrada de un hotel seguro. Apelando a la urgencia y la dificultad de manejar las cajas, presiona al guardia de seguridad para que le abra la puerta sin verificar su identificación, logrando así acceder al edificio.

## 9. Tailgating (Acceso por Seguimiento)

El **tailgating** es similar al piggybacking pero se diferencia en la **falta de interacción directa o permiso explícito** por parte del empleado autorizado.

* **Mecanismo:** El atacante, sin la autorización de seguridad requerida, sigue de cerca a una persona autorizada a través de un punto de acceso seguro (ej. una puerta con lector de tarjetas) justo después de que esta la abra.
* **Explotación de la Etiqueta Social:** Los atacantes se aprovechan de la tendencia humana a mantener las puertas abiertas a los demás o a no cuestionar a alguien que simplemente parece "pertenecer" al lugar.
* **Falsas Apariencias:** El atacante puede simular intentar abrir la puerta con una tarjeta falsa, o simplemente caminar de forma convincente como si tuviera derecho a entrar.

**Ejemplo :** En un extracto de la película de James Bond "Diamantes para la eternidad", James Bond espera a que un científico real use su tarjeta de acceso para abrir una puerta segura. Justo cuando la puerta se abre, Bond se adelanta, fingiendo deslizar su propia tarjeta (falsa), y entra por la puerta antes de que se cierre, sin que el científico note la falta de autenticación real.

## 10. Shoulder Surfing (Espionaje por Encima del Hombro)

El **shoulder surfing** es una técnica de obtención de información sensible mediante la **observación directa** del objetivo.

* **Mecanismo:** Un atacante observa el teclado, la pantalla o los movimientos del objetivo para capturar información confidencial.
* **Escenarios Comunes:**
  * **Cajeros Automáticos (ATMs):** Observar a alguien ingresar su PIN.
  * **Oficinas:** Espiar a un empleado mientras introduce su contraseña o datos sensibles en su ordenador.
  * **Lugares Públicos:** Mirar por encima del hombro en cafeterías o aeropuertos para obtener información de pantallas de portátiles o móviles.
* **Prevención:** Uso de **filtros de privacidad** en pantallas, posicionamiento consciente del cuerpo, y la práctica de ser consciente del entorno al manejar información sensible.

**Ejemplo :** Un atacante se sitúa cerca de un empleado en un área de trabajo abierta y observa cuidadosamente cómo el empleado teclea su contraseña para iniciar sesión en el sistema corporativo.

## 11. Dumpster Diving (Buceo en la Basura)

El **dumpster diving** es una técnica que implica la **recopilación de información sensible revisando la basura** de una empresa o individuo.

* **Mecanismo:** Los atacantes buscan documentos desechados que contengan información valiosa. A menudo, las empresas tiran documentos muy sensibles (listas de empleados, organigramas, detalles de proyectos, contraseñas escritas, planos de red) sin una trituración adecuada.
* **Riesgo:** La información obtenida puede ser utilizada para ataques de ingeniería social más avanzados, suplantación de identidad o para obtener conocimiento sobre la infraestructura interna de la organización.

**Ejemplo :** Un ingeniero social revisa los contenedores de basura de una empresa y encuentra un memorándum interno que detalla la estructura de la red, los nombres de los servidores y las direcciones IP, o incluso hojas con nombres de usuario y contraseñas temporales.

## 12. Suplantación de Identidad (Impersonation)

La **suplantación de identidad** es una técnica fundamental en ingeniería social que implica que un atacante se haga pasar por otra persona o entidad para engañar a la víctima.

* **Mecanismo:**
  * **Uso de Credenciales Robadas:** Un ingeniero social puede emplear credenciales obtenidas ilícitamente (ej. a través de _phishing_ o recolección de credenciales) para acceder a una red o sistema, actuando como si fuera el usuario legítimo.
  * **Suplantación de Persona:** El atacante se disfraza o simula ser alguien con autoridad, confianza o influencia (ej. el CEO de una empresa, un contratista externo, un técnico de TI) para obtener información o acceso.
* **Contexto Técnico (Man-in-the-Middle):** En un contexto más técnico, la suplantación de identidad puede manifestarse como un **ataque de intermediario (Man-in-the-Middle - MitM)**. Aquí, el atacante intercepta la comunicación entre dos víctimas, falsifica la identidad de una o ambas partes, y retransmite mensajes alterados para engañarlas y obtener información.

**Ejemplo :** Un atacante, tras obtener las credenciales de un gerente, se hace pasar por él en un correo electrónico para solicitar a un empleado del departamento de contabilidad que realice una transferencia bancaria urgente a una cuenta fraudulenta.

## 13. Recolección de Credenciales (Credential Harvesting)

La **recolección de credenciales** es el proceso mediante el cual un ingeniero social obtiene nombres de usuario y contraseñas u otra información de autenticación.

* **Mecanismo:** A menudo, se utilizan campañas de **phishing** y **spam** diseñadas específicamente para engañar a los usuarios y que introduzcan sus credenciales en sitios web falsos o las envíen a los atacantes.
* **Herramientas:** Este proceso suele implicar el uso de _software_ automatizado, programas, _scripts_ y _malware_ (como _keyloggers_ o troyanos) para facilitar la captura de información.
* **Propósito:** Las credenciales recolectadas pueden ser vendidas en el mercado negro, utilizadas para suplantación de identidad o para obtener acceso directo a sistemas y redes.

**Ejemplo :** Una campaña de _phishing_ masiva envía correos electrónicos que simulan ser de un popular servicio de almacenamiento en la nube, solicitando a los usuarios que "actualicen su información de pago". El enlace lleva a una página de _login_ falsa que captura las credenciales de acceso de los usuarios.

## 14. Pharming

El **pharming** es una técnica de ataque que redirige a las víctimas a un **sitio web malicioso** sin que estas lo perciban, incluso si escriben la dirección URL correcta.

* **Mecanismo Principal: Envenenamiento de Caché DNS (DNS Cache Poisoning):** Los atacantes manipulan las entradas en un servidor DNS (Sistema de Nombres de Dominio) o en el caché DNS local de la víctima. Esto hace que, al intentar acceder a un sitio web legítimo (ej. `www.banco.com`), el navegador del usuario sea redirigido a una página web fraudulenta controlada por el atacante.
* **Objetivo:** Robar credenciales, instalar _malware_ o realizar otras acciones maliciosas sin que la víctima se dé cuenta de que no está en el sitio correcto.
* **Sigilo:** Es particularmente peligroso porque la redirección ocurre antes de que la solicitud llegue al sitio web legítimo, lo que dificulta la detección por parte del usuario.

**Ejemplo :** Un atacante compromete un servidor DNS y modifica la entrada para `www.bancofalso.com`. Cuando los usuarios intentan acceder al banco, su navegador los envía al sitio falso, donde, a pesar de que la URL en la barra de direcciones parece correcta, todas las credenciales ingresadas son capturadas por el atacante.

## 15. Ataque de Abrevadero (Watering Hole Attack)

El **ataque de abrevadero** se enfoca en comprometer a un **grupo específico de usuarios finales** al infectar los sitios web que ese grupo visita frecuentemente, o al crear sitios nuevos diseñados para atraerlos.

* **Mecanismo:**
  1. **Identificación del Objetivo:** El atacante investiga qué sitios web son visitados regularmente por su grupo objetivo (ej. empleados de una empresa específica, miembros de un foro especializado, usuarios de un _software_ particular).
  2. **Compromiso del Sitio:** Se explota una vulnerabilidad en uno de esos sitios legítimos para inyectar _malware_ (ej. _exploits_ de _zero-day_, _scripts_ maliciosos).
  3. **Atracción:** Alternativamente, el atacante crea un sitio web nuevo y atractivo para el grupo objetivo y lo promociona para que lo visiten.
* **Resultado:** Cuando un usuario del grupo objetivo visita el sitio comprometido, su sistema es infectado automáticamente con _malware_ sin necesidad de interacción directa.

**Ejemplo :** Un grupo de ciberespionaje dirigido a investigadores de seguridad monitorea los foros y blogs técnicos que estos suelen visitar. Comprometen uno de estos sitios de confianza con un _exploit_ que se activa al cargar la página, instalando _malware_ altamente sigiloso en los ordenadores de los investigadores visitantes.

## 16. Typosquatting / Secuestro de URL

El **typosquatting**, también conocido como secuestro de URL o "secuestro de marca", explota los errores tipográficos de los usuarios al escribir direcciones web.

* **Mecanismo:** Los _hackers_ registran nombres de dominio que son deliberadamente **mal escritos** o muy similares a sitios web populares y legítimos.
* **Similitud Visual:** Los sitios web fraudulentos a menudo tienen una **interfaz de inicio de sesión idéntica** o muy similar a la del sitio original (ej. `facebook.com` vs. `FAQbook.com`, `instagram.com` vs. `instagam.com`).
* **Objetivo:** Capturar credenciales de inicio de sesión u otra información sensible de usuarios que cometen errores tipográficos o no prestan suficiente atención a la URL.

**Ejemplo :** Un usuario intenta acceder a Facebook y, por error, teclea `fackbook.com`. En lugar de obtener un error de página, es dirigido a un sitio falso idéntico visualmente, donde ingresa sus credenciales, que son capturadas por el atacante.

## 17. Campañas de Influencia (Influence Campaigns)

Las **campañas de influencia** son programas de gran escala lanzados por adversarios altamente capacitados (ej. actores estado-nación, grupos terroristas) con el objetivo de **cambiar la opinión pública** sobre un tema particular.

* **Mecanismo:** Utilizan una combinación de:
  * **Espionaje:** Recopilación de inteligencia para identificar puntos sensibles o narrativas efectivas.
  * **Desinformación / Noticias Falsas (Fake News):** Creación y difusión de contenido engañoso o completamente fabricado.
  * _**Hacking**_**:** Compromiso de cuentas o sistemas para amplificar el mensaje o acceder a información que pueda usarse para desacreditar a oponentes.
* **Contexto:** Cuando se despliegan junto con _hacking_, pueden caracterizarse como una forma de **guerra híbrida**, donde las operaciones cibernéticas se combinan con la manipulación psicológica a nivel social.
* **Impacto:** Pueden influir en elecciones políticas, movimientos sociales, percepción de marcas o decisiones estratégicas, aprovechando la difusión de información a través de medios digitales y redes sociales.

**Ejemplo :** Durante unas elecciones, un estado-nación crea una red de cuentas falsas en redes sociales para difundir noticias falsas sobre un candidato o para exacerbar divisiones sociales, con el objetivo de influir en el resultado electoral. Aunque la atribución es compleja, estos incidentes han sido objeto de debate en eventos como las elecciones presidenciales de EE. UU. de 2016.
