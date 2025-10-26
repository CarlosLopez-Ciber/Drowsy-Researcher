# Variables

En Python, una **variable** es la base para guardar y gestionar datos en tu programa. Piénsalo como una **etiqueta** o un **contenedor** en la memoria que "apunta" a un valor (como texto, un número, una lista, etc.).

> En términos simples, una variable actúa como un contenedor que guarda información temporalmente para ser usada o modificada más adelante.

***

### <mark style="color:orange;">¿Cómo se Crea y Asigna una Variable?</mark>

En Python, crear una variable es tan simple como darle un nombre y asignarle un valor usando el operador de asignación `=`.

```
mensaje = "¡Hola mundo en Python!"
print(mensaje)

# Output: ¡Hola mundo en Python!
```

* `mensaje`: Es el nombre de la variable.
* `=`: Es el operador de asignación.
* `"¡Hola mundo en Python!"`: Es el valor (un `str` o cadena) que se está almacenando.

***

### <mark style="color:orange;">Python es de Tipado Dinámico</mark>

A diferencia de otros lenguajes (como C++ o Java), en Python **no necesitas declarar el tipo de la variable** con antelación. Python infiere el tipo automáticamente cuando le asignas un valor.

Esto también significa que puedes "reasignar" un nuevo valor a una variable en cualquier momento, e incluso cambiar su tipo.

```
# 'mensaje' primero almacena un string
mensaje = "¡Hola mundo en Python!"
print(mensaje)

# Ahora, 'mensaje' almacena un string diferente
mensaje = "Aprendiendo Python paso a paso"
print(mensaje)

# Incluso podría cambiar a un número
mensaje = 100
print(mensaje)
```

**Salida esperada:**

```
¡Hola mundo en Python!
Aprendiendo Python paso a paso
100
```

***

### <mark style="color:orange;">Reglas para Nombrar Variables</mark>

Elegir buenos nombres es crucial para que tu código sea legible. Python tiene reglas estrictas (sintaxis) y recomendaciones (buenas prácticas).

#### <mark style="color:red;">🔴 Reglas Obligatorias (Sintaxis)</mark>

Si no sigues estas reglas, tu código fallará con un `SyntaxError`.

* **Debe** comenzar con una letra (`a-z`, `A-Z`) o un guion bajo (`_`).
* El resto del nombre solo puede contener letras, números (`0-9`) y guiones bajos.
* **No puede** comenzar con un número (ej. `2variable` ❌).
* **No puede** contener espacios (ej. `nombre completo` ❌).
* **No puede** usar caracteres especiales (ej. `$nombre`, `&edad` ❌).
* **No puede** ser una [palabra reservada de Python](https://www.google.com/search?q=https://es.wikibooks.org/wiki/Python/Palabras_reservadas) (ej. `print`, `if`, `def` ❌).

#### <mark style="color:purple;">🟢 Buenas Prácticas (Semántica)</mark>

Estas son convenciones de la comunidad de Python (definidas en el [PEP 8](https://peps.python.org/pep-0008/)) que hacen tu código más limpio y fácil de leer para otros programadores.

| **Práctica**                        | **Ejemplo Correcto (Recomendado)** | **Ejemplo Incorrecto (Evitar)**  |
| ----------------------------------- | ---------------------------------- | -------------------------------- |
| Nombres cortos y descriptivos       | `usuario_activo`                   | `x`, `ua` (demasiado corto)      |
| Usar **snake\_case**                | `nombre_usuario`                   | `NombreUsuario`, `nombreusuario` |
| Claridad ante todo                  | `contador_intentos`                | `cnt`                            |
| Inglés (en proyectos colaborativos) | `first_name`                       | `primer_nombre`                  |

**snake\_case** (minúsculas con guiones bajos) es el estándar de oro en Python para nombrar variables.

**Ejemplo de buenas prácticas:**

```
nombre = "Carlos"
edad = 21
usuario_activo = True

print(f"Nombre: {nombre}")
print(f"Edad: {edad}")
print(f"¿Usuario activo?: {usuario_activo}")
```

**Salida:**

```
Nombre: Carlos
Edad: 21
¿Usuario activo?: True
```

***

### <mark style="color:orange;">Asignación Múltiple: Un Atajo Útil</mark>

Python te permite asignar valores a múltiples variables en una sola línea, lo que puede ser muy conveniente.

```
# Inicializar varias variables a la vez
x, y, z = 0, 10, 20

print(f"X: {x}, Y: {y}, Z: {z}")
# Output: X: 0, Y: 10, Z: 20
```

## <mark style="color:yellow;">Constantes</mark>

Una _constante_ es una variable cuyo valor permanece igual durante toda la vida de un programa. _Utiliza las letras mayúsculas_ para indicar que una variable debe tratarse como una constante y nunca cambiarse:

```python
CONEXIONES_MAXIMAS = 5000
```
