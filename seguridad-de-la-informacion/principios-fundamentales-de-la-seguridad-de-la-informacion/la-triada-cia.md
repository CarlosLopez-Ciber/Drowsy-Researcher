# La Tríada CIA

## 1.0 El Modelo Canónico de Seguridad

La Tríada CIA es el modelo base para el diseño de políticas y sistemas de seguridad. Sus tres componentes son **Confidencialidad, Integridad y Disponibilidad**.

### 1.1 Confidencialidad (Confidentiality)

La confidencialidad es el principio que garantiza que la información no sea divulgada a individuos, entidades o procesos no autorizados. Su objetivo es prevenir el acceso no permitido a datos sensibles.

* **Mecanismos de Control:**
  * **Cifrado (Encryption):** Algoritmos que convierten datos legibles (plaintext) en un formato ininteligible (ciphertext).
  * **Control de Acceso:** Políticas y tecnologías como listas de control de acceso (ACLs), contraseñas, biometría y Autenticación Multifactor (MFA).
*   Ejemplo:

    Un informe financiero se cifra mediante el estándar AES-256 antes de ser enviado por correo electrónico. Aunque el correo sea interceptado, un atacante no podrá leer el contenido del informe sin la clave de descifrado, preservando así su confidencialidad.

### 1.2 Integridad (Integrity)

La integridad se refiere a mantener la consistencia, exactitud y fiabilidad de los datos a lo largo de todo su ciclo de vida. Los datos no deben ser alterados de forma no autorizada durante su almacenamiento, procesamiento o transmisión.

* **Mecanismos de Control:**
  * **Funciones Hash:** Algoritmos (ej. SHA-256) que generan una cadena de longitud fija (hash) para un conjunto de datos. Cualquier cambio en los datos, por mínimo que sea, produce un hash completamente diferente.
  * **Sumas de Verificación (Checksums):** Utilizadas para detectar errores introducidos durante la transmisión o el almacenamiento.
  * **Firmas Digitales:** Garantizan tanto la integridad del documento como la autenticidad del remitente.
*   Ejemplo:

    Al descargar un archivo de instalación de software, un usuario calcula su hash SHA-256 y lo compara con el valor publicado en el sitio web oficial del desarrollador. Si los hashes coinciden, se verifica la integridad del archivo, asegurando que no ha sido modificado ni corrompido con malware.

### 1.3 Disponibilidad (Availability)

La disponibilidad asegura que los sistemas, redes y datos estén operativos y accesibles para los usuarios autorizados cuando estos los requieran.

* **Mecanismos de Control:**
  * **Redundancia:** Implementación de sistemas duplicados (ej. clústeres de servidores, configuraciones RAID para discos).
  * **Balanceo de Carga:** Distribución del tráfico de red entre múltiples servidores para evitar la sobrecarga de un único punto.
  * **Planes de Recuperación ante Desastres (DRP):** Procedimientos para restaurar servicios después de una interrupción grave.
*   Ejemplo:

    Un sitio de comercio electrónico utiliza un balanceador de carga para distribuir las solicitudes de los clientes entre un grupo de servidores web. Si un servidor falla, el tráfico se redirige automáticamente a los demás, garantizando que el sitio permanezca disponible para los compradores.

## Conceptos Extendidos de la Seguridad Moderna

Con la evolución del panorama digital, la Tríada CIA se ha ampliado para incluir otros principios cruciales.

### Privacidad (Privacy)

La privacidad es el derecho de un individuo a controlar cómo se recopila, utiliza, almacena y comparte su información personal (PII - Personally Identifiable Information). Está estrechamente relacionada con la confidencialidad, pero se enfoca en el aspecto del consentimiento y el control del titular de los datos, a menudo regulado por leyes como el GDPR o la CCPA.

### No Repudio (Non-repudiation)

El no repudio es la garantía de que un sujeto (usuario o sistema) no puede negar la autoría de una acción previamente realizada. Proporciona una prueba irrefutable del origen e integridad de los datos.

*   Ejemplo:

    Cuando una persona firma un contrato digital utilizando una firma electrónica basada en certificados, se crea una prueba criptográfica que la vincula inequívocamente a ese documento. Dicha persona no puede negar ("repudiar") haber firmado el contrato, ya que solo su clave privada única podría haber generado esa firma.

