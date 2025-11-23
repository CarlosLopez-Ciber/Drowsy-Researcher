# Arquitectura de Módulos y Biblioteca Estándar

### <mark style="color:yellow;">1. Definición y Propósito</mark>

En la ingeniería de software con Python, un **módulo** es la unidad fundamental de organización de código. Técnicamente, es cualquier archivo con extensión `.py` que encapsula definiciones de funciones, variables, constantes o clases.

Su propósito trasciende la simple agrupación de código; permite:

1. **Reutilización:** Escribir una funcionalidad una vez e importarla en múltiples scripts.
2. **Abstracción:** Ocultar la complejidad interna de una función y exponer solo su interfaz de uso.
3. **Mantenimiento:** Segmentar aplicaciones grandes en archivos manejables y lógicos.

***

### <mark style="color:yellow;">2. Roles: Consumidor vs. Desarrollador</mark>

El ciclo de vida de un módulo implica dos perspectivas distintas.

#### <mark style="color:$danger;">A. El Rol del Consumidor</mark>

El desarrollador utiliza módulos existentes (propios o de terceros) para integrar funcionalidades predefinidas sin necesidad de reescribirlas.

_Ejemplo: Uso del módulo matemático._

```python
import math

# El consumidor usa 'math' como una caja de herramientas
print(math.sqrt(16)) 
```

Aquí, `math` actúa como un contenedor lógico que garantiza el acceso unívoco a la función `sqrt`.

#### <mark style="color:$danger;">B. El Rol del Desarrollador (Creación de Módulos)</mark>

Cualquier script de Python puede ser un módulo. Para crear uno, simplemente se guarda el código en un archivo `.py`.

<mark style="color:$warning;">Paso 1: Definición (</mark><mark style="color:$warning;">`mi_matematica.py`</mark><mark style="color:$warning;">)</mark>

```python
def sumar(a, b):
    """Retorna la suma de dos números."""
    return a + b
```

<mark style="color:$warning;">Paso 2: Integración (</mark><mark style="color:$warning;">`main.py`</mark><mark style="color:$warning;">)</mark>

Desde otro archivo en el mismo directorio, se importa el módulo creado.

```python
import mi_matematica

resultado = mi_matematica.sumar(3, 5)
print(resultado) # Salida: 8
```

***

### <mark style="color:yellow;">3. Estructura Interna de un Módulo</mark>

Un módulo no es solo un contenedor de funciones. Puede encapsular diversas entidades programáticas:

* **Funciones:** Procedimientos lógicos (ej. `math.sqrt()`).
* **Variables y Constantes:** Datos almacenados (ej. `math.pi`).
* **Clases:** Plantillas para objetos complejos.

Esta estructura convierte al módulo en un **contenedor lógico** que organiza y expone estos componentes para su acceso externo.

***

### <mark style="color:yellow;">4. La Biblioteca Estándar de Python</mark>

Python se describe a menudo como un lenguaje con "pilas incluidas" (_batteries included_). Esto se refiere a su **Biblioteca Estándar**: una colección exhaustiva de módulos preinstalados que cubren una amplia gama de necesidades sin requerir instalaciones externas.

**Módulos Esenciales:**

| **Módulo**     | **Funcionalidad Principal**                                      |
| -------------- | ---------------------------------------------------------------- |
| **`math`**     | Operaciones matemáticas avanzadas y constantes trigonométricas.  |
| **`os`**       | Interacción con el sistema operativo (rutas, archivos, entorno). |
| **`sys`**      | Acceso a parámetros del intérprete y argumentos del sistema.     |
| **`datetime`** | Gestión de fechas, horas y zonas horarias.                       |
| **`random`**   | Generación de números pseudoaleatorios para simulaciones.        |

Para profundizar, la referencia técnica obligatoria es la documentación oficial: [Python Library Reference](https://docs.python.org/3/library/index.html).
