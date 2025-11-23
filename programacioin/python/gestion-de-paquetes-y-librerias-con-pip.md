# Gestión de Paquetes y Librerías con pip

> Antes de instalar cualquier librería que se mencione en este post y cualquiera que veas en  PyPl, por favor, lee el post de "Entornos virtuales". Te aseguro que te evitará problemas.

Una de las mayores fortalezas de Python no es el lenguaje en sí, sino su inmenso ecosistema de librerías de terceros. Aunque Python incluye una "Biblioteca Estándar" (módulos como `math`, `os`, `sys`), la gran mayoría de herramientas profesionales (como `pandas` para datos, `django` para web, o `scapy` para redes) no vienen preinstaladas.

Para acceder a estas herramientas, utilizamos [**PyPI**](https://pypi.org/) (Python Package Index), el repositorio oficial de software para el lenguaje.

**pip** es el gestor de paquetes estándar de Python. Su función es conectarse a PyPI, descargar el código solicitado y sus dependencias, e instalarlo en tu entorno local.

### <mark style="color:yellow;">Comandos Fundamentales</mark>

El comando `pip` se ejecuta desde la terminal del sistema operativo, no desde la consola interactiva de Python (`>>>`).

#### <mark style="color:$danger;">1. Instalación de Paquetes</mark>

Para instalar la última versión de una librería, utiliza `install` seguido del nombre exacto del paquete.

```bash
# Sintaxis: pip install <nombre_del_paquete>
pip install requests
```

Al ejecutar esto, verás que pip descarga no solo `requests`, sino también otros paquetes (como `urllib3` o `certifi`). Estos son **dependencias**: librerías que `requests` necesita para funcionar. pip gestiona esto automáticamente.

#### <mark style="color:$danger;">2. Instalación de Versiones Específicas</mark>

En entornos de producción, es crítico asegurar que todos usen la misma versión del software para evitar errores de compatibilidad. Puedes especificar la versión exacta usando `==`.

```bash
# Instalar la versión 2.28.0 de requests
pip install requests==2.28.0
```

También puedes usar operadores lógicos para rangos de versiones (aunque es menos común en comandos directos y más usado en archivos de configuración):

* `>=`: Mayor o igual que.
* `<`: Menor que.

#### <mark style="color:$danger;">3. Listar Paquetes Instalados</mark>

Para ver qué librerías tienes en tu entorno actual y sus versiones:

```bash
pip list
```

**Salida típica:**

```
Package            Version
------------------ ---------
certifi            2022.6.15
charset-normalizer 2.1.0
idna               3.3
requests           2.28.1
urllib3            1.26.10
```

#### <mark style="color:$danger;">4. Desinstalación</mark>

Para eliminar un paquete que ya no necesitas.

```bash
pip uninstall requests
```

El sistema pedirá confirmación (`y/n`) antes de borrar los archivos.

#### 5. Información detallada

Si quieres saber dónde está instalado un paquete o qué dependencias tiene antes de tocar nada:

```bash
pip show requests
```

### <mark style="color:yellow;">Buenas Prácticas</mark>

#### <mark style="color:$danger;">Actualización de pip</mark>

Con frecuencia verás un aviso en amarillo indicando que tienes una versión antigua de pip. Es recomendable mantenerlo actualizado para mejoras de seguridad y velocidad.

```bash
# En Windows
python -m pip install --upgrade pip

# En Linux / macOS
pip install --upgrade pip
```

#### <mark style="color:$danger;">Conflictos de Permisos</mark>

Si intentas instalar un paquete sin estar en un Entorno Virtual, es posible que recibas un error de permisos (especialmente en Linux/macOS), ya que intentarás escribir en las carpetas del sistema.

**Nunca uses `sudo pip install`** a menos que sepas exactamente lo que haces, ya que puedes romper las librerías del sistema operativo.

**Solución correcta:**

1. Usa siempre un **Entorno Virtual** (ver lección sobre `venv`).
2.  Si es obligatorio instalarlo globalmente en tu usuario, usa el flag `--user`:

    ```bash
    pip install --user requests
    ```

