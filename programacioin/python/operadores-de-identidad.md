# Operadores de Identidad

En Python, la confusión entre igualdad e identidad es común. Aunque ambos operadores parecen comparar cosas, resuelven preguntas fundamentalmente distintas:

1. **Igualdad (`==`):** Compara el **contenido** (valor). ¿Tienen los objetos los mismos datos?
2. **Identidad (`is`):** Compara la **referencia** (memoria). ¿Son las variables punteros al mismo objeto físico en la RAM?

#### <mark style="color:$danger;">Analogía de los Gemelos</mark>

Para visualizarlo, imagina dos gemelos idénticos:

* **Comparación `==`:** Si preguntas "¿Son iguales?", la respuesta es **True**. Tienen la misma altura, rostro y ADN.
* **Comparación `is`:** Si preguntas "¿Son la misma persona?", la respuesta es **False**. Son dos entidades biológicas separadas ocupando espacios diferentes.

***

### <mark style="color:yellow;">Inspección de Memoria: Función</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">`id()`</mark>

Todo objeto en Python tiene una dirección de memoria única asignada al momento de su creación. La función `id()` permite recuperar este identificador (el "número de serie" del objeto).

> `id(objeto)` → Devuelve un entero que representa la dirección de memoria.

***

### <mark style="color:yellow;">Análisis Práctico</mark>

#### <mark style="color:$danger;">Caso 1: Objetos Distintos con el Mismo Valor</mark>

En este escenario, creamos dos estructuras de datos idénticas en contenido. Python reserva dos espacios de memoria distintos.

```python
# Usamos listas para garantizar que sean objetos nuevos
lista_a = [1, 2, 3]
lista_b = [1, 2, 3]

# Inspección de direcciones (Los números variarán en cada ejecución)
print(f"ID lista_a: {id(lista_a)}")
print(f"ID lista_b: {id(lista_b)}")

# Comparación de VALOR (Contenido)
print(f"¿Valores iguales? (==): {lista_a == lista_b}")

# Comparación de IDENTIDAD (Memoria)
print(f"¿Mismo objeto? (is): {lista_a is lista_b}")
```

**Salida Típica:**

```
ID lista_a: 2483667968368
ID lista_b: 2483667968496  <-- Direcciones diferentes
¿Valores iguales? (==): True
¿Mismo objeto? (is): False
```

**Conclusión:** `lista_a` y `lista_b` son "gemelos". Valen lo mismo, pero viven en lugares diferentes.

#### <mark style="color:$danger;">Caso 2: Referencias Compartidas (Alias)</mark>

En este escenario, asignamos una variable existente a una nueva. No se crea un objeto nuevo; simplemente se crea una nueva etiqueta (puntero) al mismo objeto.

```python
# lista_a ya existe
# Asignamos lista_c para que apunte a lo mismo que lista_a
lista_c = lista_a

print(f"ID lista_a: {id(lista_a)}")
print(f"ID lista_c: {id(lista_c)}")

print(f"¿Mismo objeto? (is): {lista_a is lista_c}")
```

**Salida Típica:**

```
ID lista_a: 2483667968368
ID lista_c: 2483667968368  <-- Misma dirección
¿Mismo objeto? (is): True
```

**Conclusión:** `lista_c` es solo un alias para `lista_a`. Modificar una afectará a la otra.

***

### <mark style="color:yellow;">La Regla de Oro: Cuándo usar</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">`is`</mark>

Para mantener un código robusto y libre de errores sutiles, sigue esta directriz:

1. Usa **`==`** para comparar datos (números, strings, listas, resultados de funciones).
2. Usa **`is`** exclusivamente para comparar con **Singletons** (objetos únicos), principalmente `None`.

#### <mark style="color:$danger;">El caso de</mark> <mark style="color:$danger;"></mark><mark style="color:$danger;">`None`</mark>

En Python, `None` es un _singleton_. Solo existe una copia de `None` en la memoria durante toda la vida del programa. Por ello, comparar identidad es más eficiente y seguro que comparar igualdad.

```python
variable = None

# PRÁCTICA RECOMENDADA (PEP 8)
# Verifica identidad directa. Es más rápido.
if variable is None:
    print("Variable vacía (Identidad)")

# PRÁCTICA NO RECOMENDADA
# Funciona, pero puede ser sobreescrito si el objeto define un método __eq__ personalizado.
if variable == None:
    print("Variable vacía (Igualdad)")
```

