# Entornos Virtuales📦

En Python, los entornos virtuales (o _virtual environments_) son una herramienta esencial que te permite crear un **espacio de trabajo aislado** para cada uno de tus proyectos. Esto significa que puedes instalar dependencias específicas para un proyecto sin afectar la instalación global de Python ni a otros proyectos en tu máquina.

Imagina que es una "caja de arena" Sandbox para cada desarrollo: lo que haces dentro de ella, se queda dentro de ella.

***

### <mark style="color:orange;">¿Por qué Deberías Usar Entornos Virtuales?</mark>

Usar `venv` (el módulo estándar de Python para esto) no es opcional, es una práctica fundamental. Estas son las razones principales:

* **🧱 Aislamiento de Dependencias:** El Proyecto A puede necesitar la versión 1.0 de una librería, mientras que el Proyecto B necesita la 2.0. Sin entornos virtuales, esto crearía un conflicto irresoluble.
* **📋 Control de Versiones:** Te permite "congelar" versiones específicas de las librerías para un proyecto, asegurando que funcione de la misma manera hoy y en el futuro.
* **🤝 Colaboración Sencilla:** Facilita que otros (compañeros de trabajo, o tú mismo en otra máquina) puedan replicar tu entorno de desarrollo exacto usando un simple archivo de requisitos.
* **🛡️ Protección del Sistema:** Evitas instalar paquetes en el Python global de tu sistema, lo cual puede interferir con herramientas del sistema operativo o con otros programas.

***

### <mark style="color:orange;">Guía Práctica: Creando y Usando</mark> <mark style="color:orange;"></mark><mark style="color:orange;">`venv`</mark>

Python incluye su propio módulo para gestionar entornos virtuales llamado `venv`, que está disponible por defecto desde Python 3.3.

#### <mark style="color:green;">1. Crear el Entorno</mark>

Abre una terminal, navega a la carpeta de tu proyecto y ejecuta el siguiente comando:

```bash
# Reemplaza 'mi_entorno' con el nombre que prefieras (venv es común)
python3 -m venv mi_entorno
```

*   **Nota:** En Windows, es probable que el comando sea `python` en lugar de `python3`:



    ```bash
    python -m venv mi_entorno
    ```

Esto creará una nueva carpeta (`mi_entorno/`) que contiene todos los archivos del entorno.

#### <mark style="color:green;">2. Activar el Entorno</mark>

Una vez creado, necesitas "activarlo":

*   **En Linux o macOS:**



    ```bash
    source mi_entorno/bin/activate
    ```
*   **En Windows (cmd.exe):**



    ```powershell
    mi_entorno\Scripts\activate
    ```

Sabrás que funcionó porque **el&#x20;**_**prompt**_**&#x20;de tu terminal cambiará**, mostrando el nombre del entorno entre paréntesis, algo como esto:

`(mi_entorno) $`

#### <mark style="color:green;">3. Instalar Dependencias</mark>

Con el entorno activo, puedes usar `pip` como de costumbre. Todos los paquetes se instalarán _dentro_ de `mi_entorno` y no globalmente.

```bash
# Este paquete solo existirá dentro de 'mi_entorno'
pip install requests
```

#### <mark style="color:green;">4. Desactivar el Entorno</mark>

Cuando termines de trabajar en el proyecto, simplemente ejecuta:

```bash
deactivate
```

El _prompt_ de tu terminal volverá a la normalidad.

***

### <mark style="color:orange;">Gestionando Dependencias:</mark> <mark style="color:orange;"></mark><mark style="color:orange;">`requirements.txt`</mark>

El verdadero poder de los entornos virtuales en la colaboración proviene de poder replicarlos. Para ello, usamos un archivo llamado `requirements.txt`.

#### <mark style="color:green;">Generar el archivo</mark>

Para "congelar" la lista de todos los paquetes y sus versiones exactas que has instalado en tu entorno activo, ejecuta:

```bash
pip freeze > requirements.txt
```

Esto crea un archivo `requirements.txt` en tu carpeta.

#### <mark style="color:green;">Instalar desde el archivo</mark>

Cuando un colaborador (o tú en otra PC) obtiene tu proyecto, solo necesita crear su propio entorno, activarlo y ejecutar:

```bash
pip install -r requirements.txt
```

Esto instalará automáticamente todas las dependencias listadas en el archivo, ¡garantizando un entorno idéntico!

#### <mark style="color:green;">¡Buena Práctica! 💡</mark>

Es una práctica estándar **excluir tu carpeta de entorno virtual** (ej. `mi_entorno/`) de tu control de versiones (Git). Esta carpeta puede ser muy pesada y es específica de cada máquina.

Asegúrate de añadir el nombre de tu entorno a tu archivo `.gitignore`:

```bash
# .gitignore
mi_entorno/
```
