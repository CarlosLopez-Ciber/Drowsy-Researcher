# El Marco de Soporte AAA

Para implementar eficazmente la Tríada CIA, se utiliza el marco AAA: **Autenticación, Autorización y Trazabilidad (Accounting)**.

* **Autenticación (Authentication):** Es el proceso de **verificar la identidad** de un usuario, sistema o servicio. Responde a la pregunta: "¿Quién eres?".
* **Autorización (Authorization):** Una vez autenticada la identidad, la autorización es el proceso de **otorgar o denegar permisos** específicos a recursos. Responde a la pregunta: "¿Qué tienes permitido hacer?".
* **Trazabilidad (Accounting / Accountability):** Es el registro y seguimiento de las acciones realizadas por una identidad autenticada. Responde a la pregunta: "¿Qué hiciste?".
*   Ejemplo:

    Un empleado ingresa su nombre de usuario y contraseña, y luego un código de su aplicación móvil para acceder a la red corporativa (Autenticación). Una vez dentro, su perfil de usuario solo le permite acceder a las carpetas del departamento de Marketing, pero no a las de Finanzas (Autorización). Cada archivo que abre o modifica queda registrado en los logs del servidor con su nombre de usuario y la marca de tiempo (Trazabilidad).
