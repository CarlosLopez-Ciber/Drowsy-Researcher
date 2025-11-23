# Paquetes y Jerarquía

A medida que una aplicación crece, organizar todo el código en módulos sueltos se vuelve inmanejable. Para resolver esto, Python ofrece los **Paquetes**.

Un **paquete** es un contenedor lógico que permite organizar múltiples módulos relacionados bajo un espacio de nombres jerárquico común. Técnicamente, un paquete se representa como un **directorio** (carpeta) en el sistema de archivos que contiene módulos (`.py`) y, tradicionalmente, un archivo de inicialización especial.

<mark style="color:red;">**Diferencia Fundamental:**</mark>

* **Módulo:** Un archivo individual (`logica.py`).
* **Paquete:** Un directorio que agrupa módulos y/o subpaquetes (`sistema/`).

#### <mark style="color:$danger;">Beneficios de la Arquitectura de Paquetes</mark>

1. **Organización Semántica:** Agrupa funcionalidades por dominio (ej. `base_de_datos`, `interfaz_grafica`, `reportes`).
2. **Espacios de Nombres Jerárquicos:** Permite usar la "notación de punto" (`paquete.modulo`) para evitar colisiones de nombres entre módulos que se llamen igual pero estén en carpetas distintas.
3. **Distribución:** Facilita compartir bibliotecas completas como una sola unidad instalable.

***

### <mark style="color:yellow;">1. Estructura del Sistema de Archivos</mark>

Para que Python entienda que una carpeta es un paquete importable, debemos seguir una estructura específica.

Supongamos que estamos desarrollando una librería para análisis de datos llamada `analytics`.

```
analytics/              <-- Directorio Raíz (El Paquete)
│
├── __init__.py         <-- Archivo de Inicialización (Obligatorio/Recomendado)
├── carga.py            <-- Módulo: analytics.carga
├── limpieza.py         <-- Módulo: analytics.limpieza
└── visualizacion.py    <-- Módulo: analytics.visualizacion
```

#### <mark style="color:$warning;">Analogía Estructural</mark>

Si los módulos son **libros** con información específica, un paquete es la **estantería** etiquetada (ej. "Matemáticas") que los contiene. No se mezclan libros de cocina en la estantería de matemáticas; del mismo modo, un paquete debe tener alta cohesión (sus módulos deben estar relacionados).

***

### <mark style="color:yellow;">2. El Rol Crítico de</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">`__init__.py`</mark>

El archivo `__init__.py` es lo que distingue a un directorio común de un paquete de Python.

#### <mark style="color:$danger;">Función 1: Marcador de Paquete</mark>

Históricamente (y por buena práctica actual), la presencia de este archivo le indica al intérprete: _"Trata este directorio como un paquete importable"_.

_Nota: Desde Python 3.3 existen los "Namespace Packages" que no requieren este archivo, pero para paquetes regulares se sigue considerando un estándar obligatorio._

#### <mark style="color:$danger;">Función 2: Código de Inicialización</mark>

Este archivo **se ejecuta automáticamente** la primera vez que se importa el paquete o cualquiera de sus módulos. Se utiliza para:

1. **Inicializar variables a nivel de paquete.**
2. **Exponer módulos internos:** Puede importar funciones de los submódulos para que el usuario las acceda directamente desde el paquete (API pública).

**Ejemplo de `__init__.py`:**

```python
# analytics/__init__.py

print("Inicializando el paquete analytics...")

# Variable disponible como analytics.VERSION
VERSION = "1.0.2" 
```

***

### <mark style="color:yellow;">3. Sintaxis de Importación (Notación de Punto)</mark>

Para acceder a los módulos dentro de un paquete, utilizamos el punto `.` como separador de jerarquía.

Supongamos que estamos en un archivo `main.py` fuera de la carpeta `analytics`.

#### <mark style="color:$danger;">Estrategia A: Importación Absoluta del Módulo</mark>

Importamos la ruta completa. Es explícito pero verboso.

```python
import analytics.carga

# Uso obligatorio de la ruta completa
analytics.carga.leer_csv("datos.csv")
```

#### <mark style="color:$danger;">Estrategia B: Importación Selectiva (</mark><mark style="color:$danger;">`from`</mark><mark style="color:$danger;">)</mark>

Importamos el módulo específico al namespace actual. Es la forma más común.

```python
from analytics import limpieza

# Acceso directo al módulo
limpieza.eliminar_nulos(dataset)
```

#### <mark style="color:$danger;">Estrategia C: Importación de Funciones Específicas</mark>

Podemos bajar hasta el nivel de función dentro de un módulo dentro de un paquete.

```python
from analytics.visualizacion import graficar_barras

graficar_barras(dataset)
```

***

### <mark style="color:yellow;">4. Jerarquía Profunda (Subpaquetes)</mark>

Los paquetes pueden contener a su vez otros paquetes, creando árboles de dependencias complejos.

```
proyecto/
├── __init__.py
├── base_datos/          <-- Subpaquete
│   ├── __init__.py
│   └── conector.py
└── web/                 <-- Subpaquete
    ├── __init__.py
    └── vistas.py
```

Para usar el módulo `conector`:

```python
import proyecto.base_datos.conector
```
