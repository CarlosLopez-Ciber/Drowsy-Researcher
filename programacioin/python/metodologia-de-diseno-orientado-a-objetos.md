# Metodología de Diseño Orientado a Objetos

### <mark style="color:yellow;">El Bloqueo de la Página en Blanco</mark>

Uno de los desafíos más comunes en el desarrollo de software no es escribir la sintaxis, sino definir la arquitectura. Pasar de una idea abstracta o un requisito de negocio a una estructura concreta de código suele ser el punto de fricción para los desarrolladores noveles.

Para superar esto, existe una técnica analítica estándar conocida como **Análisis Gramatical de Requisitos** (o método de Sustantivos y Verbos). Esta técnica permite traducir lenguaje natural a estructuras de Programación Orientada a Objetos (POO).

#### Reglas de Mapeo

La técnica consiste en tomar la descripción funcional del sistema y clasificar sus palabras clave:

1. **Sustantivos (Entidades):** Se convierten en **Clases**.
2. **Verbos (Acciones):** Se convierten en **Métodos**.
3. **Adjetivos/Sustantivos posesivos (Propiedades):** Se convierten en **Atributos**.

***

### <mark style="color:yellow;">Caso de Estudio: Gestor de Contraseñas</mark>

Para ilustrar el proceso, analicemos el siguiente requisito funcional:

> "Se requiere un **Gestor de Contraseñas** que permita a un **Usuario** guardar **Entradas**. Las entradas pueden ser de tipo **Red Social** o **Banco**. El sistema debe permitir iniciar sesión y guardar los datos".

#### Fase 1: Identificación de Clases (Sustantivos)

Analizando los sustantivos del requisito, extraemos la arquitectura base:

1. **Gestor de Contraseñas:** Es la entidad controladora. Clase: `PasswordManager`.
2. **Usuario:** Entidad que interactúa con el sistema. Clase: `Usuario`.
3. **Entrada:** La unidad de información base. Clase: `Entrada`.
4. **Red Social / Banco:** Variaciones específicas de una entrada. Clases: `EntradaSocial`, `EntradaBanco`.

#### Fase 2: Definición de Comportamiento (Verbos)

Asignamos las acciones a la clase responsable de ejecutarlas.

**Clase `Entrada` (y subclases):**

* _Acción:_ Inicializarse. -> Método: `__init__`
* _Acción:_ Mostrar detalles. -> Método: `display_details()`
* _Acción:_ Convertirse a formato guardable. -> Método: `to_dict()`

**Clase `PasswordManager` (Controlador):**

* _Acción:_ Iniciar aplicación. -> Método: `run()`
* _Acción:_ Autenticar usuario. -> Método: `login()`
* _Acción:_ Crear/Eliminar datos. -> Métodos: `create_entry()`, `delete_account()`
* _Acción:_ Persistencia de datos (Cargar/Guardar). -> Métodos: `load_data()`, `save_data()`

#### Fase 3: Definición de Estado (Adjetivos/Propiedades)

Determinamos qué datos debe almacenar cada objeto para cumplir su función.

**Clase `Entrada`:**

* Necesita almacenar: `nombre_servicio`, `usuario`, `password`, `url`.

**Clase `PasswordManager`:**

* Necesita gestionar: `current_user` (quién está logueado), `users` (lista de usuarios registrados), `vaults` (lista de contraseñas cargadas).

***

### <mark style="color:yellow;">Estableciendo Relaciones entre Clases</mark>

Una vez definidos los componentes, es crucial estructurar cómo interactúan entre sí. Para ello, utilizamos dos pruebas lógicas:

#### 1. Relación de Herencia (Prueba "ES UN")

Se utiliza para especializar clases y reutilizar código.

* ¿Una `EntradaSocial` **ES UNA** `Entrada`? **Sí.**
* ¿Una `EntradaBanco` **ES UNA** `Entrada`? **Sí.**

**Conclusión:** `Entrada` será la clase padre (superclase), y `EntradaSocial` y `EntradaBanco` serán clases hijas (subclases) que heredan sus atributos y métodos.

#### 2. Relación de Composición/Agregación (Prueba "TIENE UN")

Se utiliza para objetos que contienen o gestionan a otros objetos.

* ¿Un `PasswordManager` **ES UN** `Usuario`? **No.**
* ¿Un `PasswordManager` **TIENE** `Usuarios`? **Sí.**
* ¿Un `PasswordManager` **TIENE** `Entradas`? **Sí.**

**Conclusión:** `PasswordManager` tendrá atributos que son listas de otros objetos (ej. `self.users = []`).

***

### <mark style="color:yellow;">Principio de Arquitectura: Separación de Responsabilidades</mark>

El resultado de este diseño respeta el principio de **Separation of Concerns** (SoC).

1. **Modelos de Datos (`Entrada`, `Usuario`):** Son clases pasivas. Su única responsabilidad es contener información y validar su propio estado. No saben cómo se guardan en el disco ni cómo se muestran en la interfaz gráfica.
2. **Controlador (`PasswordManager`):** Es la clase activa. Gestiona el flujo lógico, la entrada del usuario y la orquestación de los modelos. Delega las tareas de visualización a los métodos de cada objeto individual (ej. llamando a `entrada.display_details()`).

Este enfoque modular facilita el mantenimiento: si cambia la forma de mostrar una entrada, solo modificas la clase `Entrada`, sin tocar el código del `PasswordManager`.
