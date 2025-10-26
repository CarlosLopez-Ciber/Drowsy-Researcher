# Listas🐍

Una **lista** en Python es una de las estructuras de datos más versátiles. Nos permite almacenar colecciones de elementos en una sola variable, y se definen por varias características clave.

* **Ordenadas**: Los elementos conservan el orden exacto en el que fueron insertados.
* **Mutables**: Permiten modificar, agregar o eliminar elementos después de su creación.
* **Heterogéneas**: Pueden contener distintos tipos de datos (enteros, cadenas, otras listas, etc.) al mismo tiempo.
* **Estructura Lineal**: Los elementos se almacenan uno después del otro, en una secuencia ordenada.
* **Sintaxis**: Se representan mediante **corchetes** `[]` y los elementos se separan por commas `,`.

```python
# Creación de una lista simple
languages = ['python', 'java', 'c++', 'go']
print(languages)

# Output: ['python', 'java', 'c++', 'go']
```

***

### Acceso a Elementos en una Lista

Para acceder a un elemento, usamos su **índice**, que es su posición dentro de la lista.

* Los índices en Python siempre **comienzan desde 0**. El primer elemento tiene el índice `0`, el segundo el `1`, y así sucesivamente.

```python
languages = ['python', 'java', 'c++', 'go']
print(languages[0])

# Output: 'python'
```

#### 🔹 Aplicación de Métodos de Cadenas

Al acceder a un elemento de la lista (que en este caso es una cadena de texto o `str`), puedes aplicarle directamente los métodos propios de ese tipo de dato, como `.title()`, `.upper()` o `.lower()`.

```python
print(languages[0].title())  # Convierte "python" a "Python"

# Output: 'Python'
```

#### 🔹 Acceso con Índices Negativos

Python permite usar **índices negativos** para acceder a elementos desde el final. El índice `-1` es el **último elemento**, `-2` el penúltimo, etc.

```python
print(languages[-1])  # Accede al último elemento

# Output: 'go'
```

***

### Uso de f-strings con Elementos de la Lista

Puedes integrar fácilmente los elementos de una lista en cadenas de texto (como las `f-strings`) para construir mensajes dinámicos.

```python
languages = ['python', 'java', 'c++', 'go']
message = f"El primer lenguaje que aprendí fue {languages[0].title()}."

print(message)

# Output: El primer lenguaje que aprendí fue Python.
```

***

### Métodos Comunes de las Listas

Las listas tienen "métodos" integrados, que son funciones que "pertenecen" al objeto de la lista y se llaman con un punto (p.ej., `lista.append()`).

| **Método**                 | **Descripción**                                                                       |
| -------------------------- | ------------------------------------------------------------------------------------- |
| `append(elemento)`         | Añade un `elemento` al final de la lista.                                             |
| `clear()`                  | Elimina todos los elementos de la lista.                                              |
| `copy()`                   | Devuelve una copia superficial (shallow copy) de la lista.                            |
| `count(valor)`             | Devuelve el número de veces que aparece un `valor`.                                   |
| `extend(iterable)`         | Extiende la lista agregando los elementos de un `iterable` (como otra lista).         |
| `index(valor)`             | Devuelve el primer índice donde se encuentra el `valor`. Falla si el valor no existe. |
| `insert(índice, elemento)` | Inserta un `elemento` en la posición del `índice` especificado.                       |
| `pop(índice)`              | Elimina y **devuelve** el elemento en el `índice` (por defecto, el último).           |
| `remove(valor)`            | Elimina la primera aparición del `valor`. Falla si el valor no existe.                |
| `reverse()`                | Invierte el orden de la lista (modifica la lista original).                           |
| `sort()`                   | Ordena la lista (modifica la lista original).                                         |

### ¿Dudas? Usa `help(list)`

Si alguna vez olvidas un método o cómo funciona, puedes usar la función `help()` directamente en tu terminal de Python para ver la documentación oficial.

```python
help(list)
```

> Si no logras comprender la información mostrada por la documentación, copia la información y pídele a tu IA de confianza una mayor explicación.

***

### Funciones y Declaraciones Útiles

Existen también funciones y declaraciones generales de Python (que no se llaman con un punto) que son muy útiles para trabajar con listas.

#### Eliminación por Índice con la Instrucción `del`

La instrucción `del` elimina permanentemente un elemento de la lista usando su índice.

```python
languages = ['python', 'java', 'c++']
print(f"Lista antes: {languages}")

# Output: Lista antes: ['python', 'java', 'c++']

del languages[0]  # Elimina 'python'
print(f"Lista después: {languages}")

# Output: Lista después: ['java', 'c++']
```

> `del` es útil cuando sabes la posición exacta del elemento y **no necesitas conservar el valor eliminado**. A diferencia del método `.pop()`, `del` no devuelve el valor que borra.

#### Ordenar una Lista Temporalmente con `sorted()`

Si quieres ver una versión ordenada de tu lista pero **sin alterar el orden original**, puedes usar la función `sorted()`. Esta función **devuelve una nueva lista ordenada** y deja la original intacta.

```python
languages = ['python', 'java', 'go', 'c++']

print("Lista original:")
print(languages)
# Output: ['python', 'java', 'go', 'c++']

print("\nLista ordenada temporalmente:")
print(sorted(languages))
# Output: ['c++', 'go', 'java', 'python']

print("\nLista original (sigue igual):")
print(languages)
# Output: ['python', 'java', 'go', 'c++']
```

#### Encontrar la Longitud de una Lista con `len()`

La función `len()` te devuelve la **cantidad total de elementos** que contiene una lista.

```python
languages = ['python', 'java', 'go', 'rust']
print(len(languages))

# Output: 4
```

> `len()` devuelve `4` porque hay cuatro elementos. Es clave recordar que, aunque **los índices comienzan en 0** (el índice máximo es `3`), `len()` cuenta la **cantidad total de elementos** (empezando desde 1).
