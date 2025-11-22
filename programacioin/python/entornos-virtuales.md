# Entornos Virtuales

En el desarrollo con Python, los entornos virtuales (virtual environments) son una herramienta esencial que permite crear un espacio de trabajo aislado para cada proyecto. El objetivo principal es poder instalar dependencias específicas para un desarrollo sin afectar la instalación global de Python ni interferir con otros proyectos alojados en la misma máquina.

### <mark style="color:yellow;">¿Qué es un Entorno Virtual?</mark>

Técnicamente, un entorno virtual es un directorio autocontenido. Este directorio incluye:

1. Una copia funcional de la instalación de Python (el intérprete).
2. Sus propias herramientas de gestión de paquetes (`pip`).
3. Una carpeta de librerías donde se almacenarán las dependencias exclusivas de ese entorno.

Cuando se "activa" un entorno, la terminal deja de utilizar el Python global del sistema operativo y pasa a utilizar esta copia local.

### <mark style="color:yellow;">Razones para utilizar aislamiento</mark>

El uso de `venv` (el módulo estándar de Python) se considera una práctica fundamental por los siguientes motivos:

* **Aislamiento de Dependencias:** Evita conflictos de versiones. Un Proyecto A puede requerir la versión 1.0 de una librería, mientras que el Proyecto B necesita la 2.0. Los entornos virtuales permiten que ambos coexistan.
* **Control de Versiones:** Permite "congelar" el estado exacto de las librerías usadas, asegurando que el código funcione igual hoy y en el futuro.
* **Colaboración:** Facilita que otros desarrolladores repliquen el entorno de trabajo exacto.
* **Protección del Sistema:** Evita la instalación de paquetes en el Python global, lo cual podría romper herramientas del sistema operativo que dependen de versiones específicas de Python.

***

### <mark style="color:yellow;">Guía Técnica: Ciclo de vida de un entorno</mark>

Python incluye por defecto (desde la versión 3.3) el módulo `venv` para esta tarea. A continuación se detalla el proceso estándar.

#### <mark style="color:$danger;">1. Creación del entorno</mark>

Abre una terminal y navega hasta la carpeta raíz de tu proyecto. Ejecuta el siguiente comando para crear la estructura de carpetas:

```bash
# Sintaxis: python -m venv <nombre_del_entorno>
# 'venv' es el nombre estándar recomendado para la carpeta

# En Windows:
python -m venv venv

# En Linux / macOS (asegúrate de usar python3):
python3 -m venv venv
```

Este comando generará una carpeta llamada `venv/` con todos los archivos necesarios.

#### <mark style="color:$danger;">2. Activación</mark>

Para empezar a usar el entorno, es necesario activarlo. El comando varía según el sistema operativo:

*   **Windows (cmd.exe):**

    ```
    venv\Scripts\activate
    ```
*   **Windows (PowerShell):**

    ```powershell
    venv\Scripts\Activate.ps1
    ```
*   **Linux / macOS:**

    ```bash
    source venv/bin/activate
    ```

**Verificación:** Sabrás que el entorno está activo porque el prompt de tu terminal cambiará, mostrando el nombre del entorno entre paréntesis al inicio, por ejemplo: `(venv) $`.

#### <mark style="color:$danger;">3. Instalación de paquetes</mark>

Con el entorno activo, cualquier uso de `pip` afectará únicamente a la carpeta `venv`.

```bash
# Este paquete se instala solo en el entorno aislado
pip install requests
```

#### <mark style="color:$danger;">4. Desactivación</mark>

Al finalizar la sesión de trabajo, para volver al intérprete global de Python, ejecuta:

```bash
deactivate
```

***

### <mark style="color:yellow;">Gestión de dependencias para colaboración</mark>

Para compartir el proyecto o desplegarlo en un servidor, no se debe copiar la carpeta `venv`. En su lugar, se utiliza un archivo de texto para listar las dependencias.

#### <mark style="color:$danger;">Generar el archivo de requisitos (</mark><mark style="color:$danger;">`requirements.txt`</mark><mark style="color:$danger;">)</mark>

Con el entorno activo y las librerías instaladas, ejecuta:

```bash
pip freeze > requirements.txt
```

Esto creará un archivo que lista cada paquete instalado y su versión exacta.

#### <mark style="color:$danger;">Instalar desde el archivo</mark>

Si descargamos el proyecto en una nueva máquina, el flujo correcto es crear un entorno nuevo, activarlo y ejecutar:

```bash
pip install -r requirements.txt
```

Esto replicará el entorno original automáticamente.

***

### <mark style="color:yellow;">Buenas Prácticas: Control de Versiones (Git)</mark>

Es un error común subir la carpeta del entorno virtual a repositorios como GitHub. Esta carpeta es pesada y específica para cada sistema operativo.

Para evitarlo, se debe crear un archivo `.gitignore` en la raíz del proyecto y añadir el nombre del entorno:

```
# Contenido del archivo .gitignore
venv/
__pycache__/
```
