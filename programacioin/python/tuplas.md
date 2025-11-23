# Tuplas

Una **tupla** es una estructura de datos que almacena una colección ordenada de elementos. Puede contener datos heterogéneos (enteros, flotantes, cadenas, e incluso otras estructuras).

Su característica definitoria es la **inmutabilidad**: una vez creada una tupla, su contenido (longitud y elementos) no puede modificarse. No es posible añadir, eliminar o reasignar elementos.

***

### <mark style="color:yellow;">1. Sintaxis de Creación</mark>

Python ofrece flexibilidad en la definición de tuplas. Aunque los paréntesis son la convención visual, lo que realmente define a la tupla es la coma.

#### <mark style="color:$danger;">Definición Estándar (con paréntesis)</mark>

Es la forma más legible y común.

```python
tupla_1 = (1, 2, 4, 8)
```

#### <mark style="color:$danger;">Empaquetado (sin paréntesis)</mark>

Python infiere que una secuencia de valores separados por comas es una tupla.

```python
tupla_2 = 1.0, 0.5, 0.25
```

#### <mark style="color:$danger;">Casos Especiales</mark>

*   **Tupla Vacía:** Se define con paréntesis vacíos.



    ```python
    tupla_vacia = ()
    ```
*   **Tupla Unitaria (Crucial):** Para crear una tupla de un solo elemento, **es obligatorio colocar una coma final**. Sin ella, Python interpreta los paréntesis como operadores matemáticos de agrupación.



    ```python
    # Esto es un entero (int)
    no_es_tupla = (1)

    # Esto es una tupla (tuple)
    es_tupla = (1,)

    # Variante flotante sin paréntesis
    es_tupla_float = 1.0,
    ```

***

### <mark style="color:yellow;">2. Acceso y Slicing</mark>

El acceso a los elementos funciona idénticamente a las listas o cadenas, utilizando índices numéricos basados en cero.

```python
mi_tupla = (1, 10, 100, 1000)

# Acceso directo
print(mi_tupla[0])      # Salida: 1
print(mi_tupla[-1])     # Salida: 1000 (Último elemento)

# Rebanado (Slicing)
print(mi_tupla[1:])     # Salida: (10, 100, 1000)
print(mi_tupla[:2])     # Salida: (1, 10)
```

***

### <mark style="color:yellow;">3. Inmutabilidad en la Práctica</mark>

Cualquier intento de modificar la estructura interna de una tupla generará una excepción en tiempo de ejecución.

```python
datos = (1, 10, 100)

# ERROR 1: Asignación de ítems
# datos[1] = -10  
# TypeError: 'tuple' object does not support item assignment

# ERROR 2: Modificación de tamaño (append no existe)
# datos.append(1000)
# AttributeError: 'tuple' object has no attribute 'append'

# ERROR 3: Eliminación de ítems
# del datos[0]
# TypeError: 'tuple' object does not support item deletion
```

***

### <mark style="color:yellow;">4. Comparativa Técnica: Tupla vs. Lista</mark>

La elección entre usar una tupla o una lista depende del contexto del programa.

| **Característica**  | **Lista (list)**                                     | **Tupla (tuple)**                                          |
| ------------------- | ---------------------------------------------------- | ---------------------------------------------------------- |
| **Mutabilidad**     | ✅ Mutable (Modificable)                              | ❌ Inmutable (Constante)                                    |
| **Sintaxis**        | Corchetes `[]`                                       | Paréntesis `()`                                            |
| **Rendimiento**     | Ligeramente más lenta (overhead de memoria dinámico) | Ligeramente más rápida (memoria estática)                  |
| **Seguridad**       | Baja (cualquier función puede alterarla)             | Alta (integridad de datos garantizada)                     |
| **Uso Recomendado** | Colecciones de datos que cambian dinámicamente.      | Datos constantes, configuraciones o claves de diccionario. |
| **Métodos**         | Amplios (`append`, `pop`, `remove`, `sort`)          | Limitados (`count`, `index`)                               |

***

### <mark style="color:yellow;">5. Operaciones Válidas</mark>

Aunque no se pueden modificar, se pueden realizar operaciones de lectura, concatenación y repetición (estas dos últimas generan **nuevas** tuplas, no modifican la original).

```python
t = (1, 10, 100)

# Longitud
print(len(t))           # 3

# Concatenación (Crea nueva tupla)
print(t + (1000, 2000)) # (1, 10, 100, 1000, 2000)

# Repetición
print(t * 3)            # (1, 10, 100, 1, 10, 100, 1, 10, 100)

# Pertenencia (Búsqueda)
print(10 in t)          # True
print(999 not in t)     # True
```

***

### <mark style="color:yellow;">6. Desempaquetado (Unpacking)</mark>

Python permite asignar los elementos de una tupla a variables individuales en una sola línea. El número de variables debe coincidir exactamente con el número de elementos de la tupla.

```python
coordenadas = (10, 20, 30)

# Asignación múltiple
x, y, z = coordenadas

print(f"X: {x}, Y: {y}, Z: {z}")
# Salida: X: 10, Y: 20, Z: 30
```

#### <mark style="color:$danger;">Intercambio de Variables (Swap)</mark>

Gracias al empaquetado y desempaquetado de tuplas, Python permite intercambiar valores sin necesidad de una variable temporal auxiliar.

```python
a = 5
b = 10

# El lado derecho crea una tupla (10, 5)
# El lado izquierdo la desempaqueta en a y b
a, b = b, a

print(f"a: {a}, b: {b}") 
# Salida: a: 10, b: 5
```

***

### <mark style="color:yellow;">7. Contenido Dinámico</mark>

Una tupla puede contener expresiones o variables. Estas se evalúan en el momento de la creación de la tupla.

```python
x = 10
y = 20

# Tupla con expresiones aritméticas
calculos = (x + y, x * y)

print(calculos)
# Salida: (30, 200)
```
