# Diccionarios

Un **diccionario** es una colección de datos **mutable** y desordenada (semánticamente), diseñada para almacenar pares de **Clave-Valor** (_Key-Value pairs_).

A diferencia de las listas, que indexan por posición numérica (0, 1, 2...), los diccionarios indexan por una clave única definida por el programador. Técnicamente, es la implementación en Python de una Tabla Hash (_Hash Map_), lo que permite un acceso a los datos extremadamente rápido, independientemente del tamaño del diccionario.

***

### <mark style="color:yellow;">1. Sintaxis y Creación</mark>

Los diccionarios se definen mediante llaves `{}`. Cada elemento se separa por comas y la relación entre clave y valor se denota con dos puntos `:`.

#### Inicialización

```python
# Diccionario vacío (Esencial para acumuladores)
diccionario_vacio = {}

# Diccionario con datos iniciales
# Claves: Strings. Valores: Strings e Integers.
telefonos = {
    "Jefe": 5551234567,
    "Suzy": 22657854310
}
```

#### <mark style="color:$danger;">Reglas Técnicas de las Claves (</mark><mark style="color:$danger;">`Keys`</mark><mark style="color:$danger;">)</mark>

Para que un objeto sirva como clave, debe ser **hashable** (inmutable).

1. **Válido:** Enteros, Flotantes, Cadenas, Booleanos, Tuplas.
2. **Inválido:** Listas, Diccionarios (porque son mutables).
3. **Unicidad:** No puede haber claves duplicadas. Si se define una clave dos veces, la última sobrescribe a la anterior.

***

### <mark style="color:yellow;">2. Acceso y Lectura de Datos</mark>

Existen dos métodos principales para recuperar un valor.

#### <mark style="color:$danger;">Acceso Directo (Corchetes)</mark>

Es rápido, pero inseguro si no se tiene certeza de la existencia de la clave.

```python
print(telefonos["Suzy"])
# Salida: 22657854310

# Riesgo: Si la clave no existe, lanza una excepción crítica.
# print(telefonos["Presidente"]) 
# Error: KeyError: 'Presidente'
```

#### <mark style="color:$danger;">Acceso Seguro (</mark><mark style="color:$danger;">`get`</mark><mark style="color:$danger;">)</mark>

Es el método recomendado para evitar errores en tiempo de ejecución.

```python
# Si la clave no existe, devuelve None (o un valor por defecto)
resultado = telefonos.get("Presidente", "No encontrado")
print(resultado) 
# Salida: No encontrado
```

***

### <mark style="color:yellow;">3. Modificación (Mutabilidad)</mark>

Los diccionarios son dinámicos; permiten crecer, encogerse y modificar valores in situ.

#### <mark style="color:$danger;">Inserción y Actualización</mark>

No existe diferencia sintáctica entre crear y actualizar. Si la clave existe, se actualiza; si no, se crea.

```python
datos = {"gato": "chat"}

# Agregar nuevo par
datos["perro"] = "chien"

# Actualizar existente
datos["gato"] = "minou"

# Fusión masiva con .update()
datos.update({"pato": "canard", "cisne": "cygne"})
```

#### <mark style="color:$danger;">Eliminación</mark>

```python
# Eliminar una clave específica
del datos["perro"]

# Eliminar y capturar el valor (como en listas)
valor = datos.pop("gato")

# Eliminar el último elemento insertado (LIFO - Python 3.7+)
datos.popitem()
```

***

### <mark style="color:yellow;">4. Iteración y Vistas</mark>

Recorrer un diccionario es una operación fundamental. Python ofrece tres "vistas" distintas para hacerlo.

#### <mark style="color:$danger;">Iteración Estándar (Solo claves)</mark>

```python
# Equivale a: for k in datos.keys():
for k in datos:
    print(k)
```

#### <mark style="color:$danger;">Iteración de Pares (</mark><mark style="color:$danger;">`items`</mark><mark style="color:$danger;">) - La forma "Pythonic"</mark>

Permite desempaquetar la clave y el valor simultáneamente en el bucle.

```python
traducciones = {"rojo": "red", "azul": "blue"}

for clave, valor in traducciones.items():
    print(f"{clave} -> {valor}")
```

**Salida:**

```
rojo -> red
azul -> blue
```

#### <mark style="color:$danger;">Iteración Ordenada</mark>

Dado que los diccionarios no garantizan un orden semántico estricto en versiones antiguas, para reportes se recomienda ordenar las claves.

```python
for k in sorted(traducciones.keys()):
    print(f"{k}: {traducciones[k]}")
```

***

### <mark style="color:yellow;">5. Buenas Prácticas de Estilo</mark>

Para diccionarios extensos o configuraciones, se recomienda la "Sangría Francesa" para alinear visualmente las claves y valores, mejorando la legibilidad vertical.

```python
configuracion = {
    "host":     "127.0.0.1",
    "port":     8080,
    "debug":    True,
    "timeout":  30
}
```

***

### <mark style="color:yellow;">6. Referencia de Métodos</mark>

| **Método**         | **Descripción**                                                          |
| ------------------ | ------------------------------------------------------------------------ |
| `keys()`           | Retorna una vista iterable de las claves.                                |
| `values()`         | Retorna una vista iterable de los valores.                               |
| `items()`          | Retorna una vista de tuplas `(clave, valor)`.                            |
| `get(k, d)`        | Retorna el valor de `k`. Si no existe, retorna `d` (por defecto `None`). |
| `setdefault(k, v)` | Si `k` existe, devuelve su valor. Si no, inserta `k` con valor `v`.      |
| `update(dict2)`    | Añade los pares de `dict2` al diccionario actual.                        |
| `pop(k)`           | Elimina la clave `k` y devuelve su valor.                                |
| `popitem()`        | Elimina y devuelve el último par insertado `(clave, valor)`.             |
| `clear()`          | Vacía el diccionario por completo.                                       |
| `len(d)`           | Devuelve la cantidad de pares almacenados.                               |
| `k in d`           | Devuelve `True` si la clave `k` existe en el diccionario `d`.            |
