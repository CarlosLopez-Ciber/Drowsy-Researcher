# Variables

En Python, una **variable** es el mecanismo fundamental para almacenar y gestionar datos. Técnicamente, actúa como una referencia o "etiqueta" en la memoria del sistema que apunta a un valor específico (un número, una cadena de texto, una lista, etc.).

A diferencia de otros lenguajes que tratan las variables como cajas de tamaño fijo, Python las trata como referencias a objetos.

### <mark style="color:yellow;">Creación y Asignación</mark>

Para crear una variable, se utiliza el operador de asignación `=`. La sintaxis es `nombre_variable = valor`.

```python
mensaje = "Hola mundo en Python"
print(mensaje)
# Salida: Hola mundo en Python
```

En este bloque:

1. `mensaje`: Es el identificador (nombre) de la variable.
2. `=`: Es el operador que asigna el valor de la derecha al nombre de la izquierda.
3. `"Hola mundo..."`: Es el objeto (dato) almacenado en memoria.

***

### <mark style="color:yellow;">Tipado Dinámico</mark>

Python utiliza un sistema de **tipado dinámico**. Esto implica dos características:

1. No es necesario declarar el tipo de dato explícitamente (no se usa `int x` o `String s`).
2. Una misma variable puede cambiar de tipo durante la ejecución del programa al asignarle un nuevo valor.

```python
# Inicialización como cadena de texto (str)
dato = "Aprendiendo Python"
print(dato)

# Reasignación como entero (int)
dato = 100
print(dato)
```

**Salida:**

```
Aprendiendo Python
100
```

***

### <mark style="color:yellow;">Reglas de Nomenclatura</mark>

Para nombrar variables correctamente, se deben distinguir las reglas obligatorias de sintaxis (que causan errores si no se siguen) y las convenciones de estilo (que mejoran la legibilidad).

#### <mark style="color:$danger;">Reglas de Sintaxis (Obligatorias)</mark>

Si se violan estas reglas, el intérprete arrojará un `SyntaxError`.

* **Caracteres permitidos:** Letras (a-z, A-Z), números (0-9) y guiones bajos (`_`).
* **Inicio:** El nombre debe comenzar obligatoriamente con una letra o un guion bajo. **Nunca** con un número (ej. `2variable` es inválido).
* **Espacios:** No se permiten espacios en blanco (ej. `nombre usuario` es inválido).
* **Palabras Reservadas:** No se pueden usar palabras clave del lenguaje como identificadores (ej. `class`, `return`, `if`, `global`).

#### <mark style="color:$danger;">Convenciones de Estilo (PEP 8)</mark>

La guía de estilo oficial de Python (PEP 8) recomienda estándares para mantener el código limpio y consistente.

* **Snake Case:** Las variables deben escribirse en minúsculas, separando las palabras con guiones bajos (`nombre_de_usuario`).
* **Descriptividad:** Los nombres deben ser claros y explicar el contenido de la variable.

| **Tipo**     | **Ejemplo Correcto (Recomendado)**        | **Ejemplo Incorrecto (Evitar)**  |
| ------------ | ----------------------------------------- | -------------------------------- |
| **Formato**  | `nombre_usuario`                          | `NombreUsuario`, `nombreusuario` |
| **Claridad** | `contador_intentos`                       | `cnt`, `c`                       |
| **Idioma**   | `first_name` (en equipos internacionales) | `primer_nombre`                  |

**Ejemplo de aplicación de buenas prácticas:**

```python
nombre_completo = "Carlos Pérez"
edad_usuario = 21
esta_activo = True

print(f"Usuario: {nombre_completo}, Edad: {edad_usuario}, Activo: {esta_activo}")
```

***

### <mark style="color:yellow;">Asignación Múltiple</mark>

Python permite asignar valores a varias variables en una sola línea de código, lo cual es útil para inicializar coordenadas o valores relacionados.

```python
# Asignación posicional: x=0, y=10, z=20
x, y, z = 0, 10, 20

print(f"X: {x}, Y: {y}, Z: {z}")
# Salida: X: 0, Y: 10, Z: 20
```

***

### <mark style="color:yellow;">Constantes</mark>

Una **constante** es un valor que no debería cambiar durante la ejecución del programa.

Python no tiene un tipo de dato "constante" estricto que impida la modificación del valor a nivel de intérprete (como `const` en otros lenguajes). Sin embargo, existe una convención universalmente respetada:

**Las constantes se escriben completamente en MAYÚSCULAS.**

Al ver una variable en mayúsculas, el programador sabe que no debe modificar ese valor.

```python
# Convención de constante
CONEXIONES_MAXIMAS = 5000
PI = 3.14159

print(CONEXIONES_MAXIMAS)
```
