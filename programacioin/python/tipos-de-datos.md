# Tipos de Datos

En Python, todo es un objeto, y cada objeto tiene un **tipo** (o "clase"). Aunque Python tiene **tipado dinámico** (no tienes que _declarar_ el tipo de una variable), internamente sabe perfectamente qué tipo de dato estás manejando.

El tipo le dice a Python qué operaciones son válidas. Por ejemplo, puedes "sumar" (`+`) dos números, pero no puedes "sumar" un número y una palabra.

Para saber qué tipo de dato tiene una variable, usamos la función `type()`.

```python
variable = "Hola"
print(type(variable))
# Output: <class 'str'>

variable = 100
print(type(variable))
# Output: <class 'int'>
```

***

### 1. Tipos Numéricos

Se usan para almacenar valores numéricos.

* **Enteros (`int`):** Números enteros, positivos o negativos, sin decimales.
* **Flotantes (`float`):** Números con punto decimal.
* **Complejos (`complex`):** Números con una parte real y una imaginaria (indicada con una `j`). Son usados en matemáticas avanzadas.

```python
un_entero = 42
un_flotante = 3.1416
un_complejo = 3 + 5j

print(type(un_entero))    # Output: <class 'int'>
print(type(un_flotante))  # Output: <class 'float'>
print(type(un_complejo))  # Output: <class 'complex'>
```

***

### 2. Tipo de Texto

* **Cadena (`str`):** Se usa para almacenar texto. El valor se encierra entre comillas simples (`'...'`) o dobles (`"..."`).

```python
saludo = "Hola Mundo"
otro_texto = 'Python 3'
numero_como_texto = "12345" # ¡Esto es texto, no un número!

print(type(saludo))             # Output: <class 'str'>
print(type(numero_como_texto))  # Output: <class 'str'>
```

***

### 3. Tipos de Secuencia

Se usan para almacenar colecciones ordenadas de elementos. El orden de inserción se mantiene.

* **Listas (`list`):** Una colección ordenada y **mutable** (puedes cambiar, añadir o eliminar elementos). Se definen con corchetes `[]`.
* **Tuplas (`tuple`):** Una colección ordenada e **inmutable** (no puedes cambiar sus elementos una vez creada). Se definen con paréntesis `()`. Son más rápidas que las listas y se usan para datos que no deben cambiar.
* **Rango (`range`):** Representa una secuencia inmutable de números, comúnmente usada para bucles `for`.

```python
mi_lista = [1, "manzana", 3.0, True]
mi_tupla = (1, "manzana", 3.0, True)
mi_rango = range(10) # Números del 0 al 9

print(type(mi_lista))  # Output: <class 'list'>
print(type(mi_tupla))  # Output: <class 'tuple'>
print(type(mi_rango))  # Output: <class 'range'>

# Las listas son mutables
mi_lista[0] = 99
print(mi_lista)      # Output: [99, 'manzana', 3.0, True]
```

***

### 4. Tipo de Mapeo

Se usa para almacenar colecciones de pares `clave: valor`.

* **Diccionario (`dict`):** Es una colección **mutable**. En lugar de acceder por un índice numérico (como las listas), accedes a un valor a través de su **clave** única. Se definen con llaves `{}`.
  * _Nota: Desde Python 3.7+, los diccionarios también mantienen el orden de inserción._

```python
# La clave es "nombre", el valor es "Ana".
persona = {
    "nombre": "Ana",
    "edad": 25,
    "ciudad": "Lima"
}

print(type(persona))      # Output: <class 'dict'>
print(persona["nombre"])  # Output: 'Ana'
```

***

### 5. Tipos de Conjunto

Se usan para almacenar colecciones no ordenadas de elementos **únicos**. Su gran ventaja es que eliminan duplicados automáticamente.

* **Conjunto (`set`):** Una colección no ordenada y **mutable** de elementos únicos.
* **Conjunto Inmutable (`frozenset`):** Similar a `set`, pero es **inmutable** una vez creado.

```python
lista_con_duplicados = [1, 2, 2, 3, 3, 3, "a", "a"]
mi_set = set(lista_con_duplicados)

print(type(mi_set)) # Output: <class 'set'>
print(mi_set)       # Output: {1, 2, 3, 'a'} (¡Sin duplicados!)
```

***

### 6. Tipo Booleano

Se usa para representar valores de verdad. Es el pilar de la toma de decisiones (`if`) y los bucles (`while`).

* **Booleano (`bool`):** Solo puede tener dos valores: `True` (verdadero) o `False` (falso). (¡Ojo con las mayúsculas iniciales!)

```python
activo = True
encontrado = False

print(type(activo)) # Output: <class 'bool'>
```

***

### 7. Tipo Nulo

Se usa para representar la ausencia total de valor.

* **NoneType (`None`):** Tiene un único valor, `None`. Se usa a menudo para inicializar una variable antes de asignarle un valor real o para indicar que una función no devuelve nada.

```python
resultado = None

print(type(resultado)) # Output: <class 'NoneType'>
```
