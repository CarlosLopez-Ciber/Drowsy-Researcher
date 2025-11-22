# Operadores de Asignación

El operador de asignación fundamental en Python es el signo igual (`=`). Su función no es "igualdad matemática", sino **vinculación**: asocia un nombre (variable) a un objeto en memoria.

```python
puntuacion = 100
```

Frecuentemente, necesitamos actualizar una variable basándonos en su valor actual (acumuladores, contadores, etc.).

```python
# Forma verbosa
puntuacion = puntuacion + 10
```

Para optimizar esta operación, Python ofrece la **Asignación Aumentada** (_Augmented Assignment_).

***

### Sintaxis de Asignación Aumentada

Esta sintaxis combina un operador binario (como suma o resta) con la asignación en un solo paso atómico.

* **Sintaxis:** `variable OPERADOR= valor`
* **Significado:** "Aplica la operación sobre la variable y guarda el resultado en la misma variable".

```python
puntuacion = 100
puntuacion += 10  # Equivale a: puntuacion = puntuacion + 10

print(puntuacion)
# Salida: 110
```

### Tabla de Referencia

Estos operadores están disponibles para toda la aritmética estándar:

| **Operador** | **Descripción**          | **Ejemplo (Atajo)** | **Equivalente Lógico** |
| ------------ | ------------------------ | ------------------- | ---------------------- |
| `+=`         | Suma y asigna            | `x += 5`            | `x = x + 5`            |
| `-=`         | Resta y asigna           | `x -= 5`            | `x = x - 5`            |
| `*=`         | Multiplica y asigna      | `x *= 5`            | `x = x * 5`            |
| `/=`         | Divide y asigna          | `x /= 5`            | `x = x / 5`            |
| `//=`        | División entera y asigna | `x //= 5`           | `x = x // 5`           |
| `%=`         | Módulo y asigna          | `x %= 5`            | `x = x % 5`            |
| `**=`        | Potencia y asigna        | `x **= 5`           | `x = x ** 5`           |

***

### Diferencia Técnica Crítica: Mutabilidad

Es un error común pensar que `a += b` es _exactamente_ lo mismo que `a = a + b`. Aunque el resultado visual suele ser el mismo, **el comportamiento en memoria es diferente** dependiendo de si el objeto es mutable o inmutable.

#### 1. Con Objetos Inmutables (Enteros, Strings)

Como el objeto no puede cambiar, Python calcula el nuevo valor, crea un nuevo objeto y actualiza la referencia. Aquí, `+=` se comporta igual que la asignación normal.

```python
a = 10
id_original = id(a)

a += 5 

print(a)           # 15
print(id(a) == id_original) # False (Es un nuevo objeto)
```

#### 2. Con Objetos Mutables (Listas)

Aquí radica la diferencia importante.

* `lista = lista + [...]`: Crea una **nueva lista** y reasigna la variable.
* `lista += [...]`: Modifica la lista original **in-situ** (similar a `.extend()`).

```python
# Caso A: Asignación normal (Crea copia)
lista_1 = [1, 2]
id_1 = id(lista_1)
lista_1 = lista_1 + [3] 
print(id(lista_1) == id_1) # False (Objeto nuevo, referencia rota)

# Caso B: Asignación Aumentada (Modificación in-situ)
lista_2 = [1, 2]
id_2 = id(lista_2)
lista_2 += [3]
print(id(lista_2) == id_2) # True (Mismo objeto modificado)
```

> **Nota de Rendimiento:** En listas grandes, usar `+=` es mucho más rápido y eficiente en memoria que `lista = lista + ...`, ya que evita crear una copia completa de la lista solo para agregar un elemento.
