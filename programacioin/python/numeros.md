# Números

Los números constituyen la base del cómputo, utilizados para todo, desde el control de bucles hasta el análisis de datos complejos. En Python, existen dos tipos numéricos fundamentales que se utilizan constantemente:

* **Enteros (`int`):** Números completos sin parte decimal (ej. `10`, `-5`, `2000`). Tienen precisión ilimitada (solo restringida por la memoria de la máquina).
* **Flotantes (`float`):** Números con parte decimal o notación científica (ej. `3.14`, `1.5`, `-0.001`).

***

### <mark style="color:yellow;">1. Números Enteros (</mark><mark style="color:yellow;">`int`</mark><mark style="color:yellow;">)</mark>

Los enteros permiten realizar las operaciones aritméticas estándar de forma directa.

```python
print(2 + 3)   # Suma
print(3 - 2)   # Resta
print(2 * 3)   # Multiplicación
```

**Salida:**

```
5
1
6
```

#### <mark style="color:$danger;">Potencias (Exponentes)</mark>

A diferencia de otros lenguajes que usan funciones como `pow()`, Python incluye un operador nativo para la potenciación: el doble asterisco (`**`).

```python
print(3 ** 2)   # 3 al cuadrado (9)
print(10 ** 6)  # 10 a la sexta (1000000)
```

#### <mark style="color:$danger;">Jerarquía de Operaciones (PEMDAS)</mark>

Python respeta estrictamente el orden matemático estándar:

1. Paréntesis
2. Exponentes
3. Multiplicación / División
4. Adición / Sustracción

```python
# Multiplicación (3 * 4) tiene prioridad sobre la suma
print(2 + 3 * 4)
# Salida: 14

# Los paréntesis fuerzan la prioridad de la suma
print((2 + 3) * 4)
# Salida: 20
```

**Buenas Prácticas:** Aunque los espacios no afectan la ejecución (`2+3*4`), se recomienda utilizarlos (`2 + 3 * 4`) para mejorar la legibilidad. Asimismo, usa paréntesis para hacer explícita la intención del cálculo, incluso si no son estrictamente necesarios.

#### <mark style="color:$danger;">Separadores Visuales (Python 3.6+)</mark>

Para mejorar la lectura de cifras grandes, Python permite el uso de guiones bajos (`_`) como separadores de miles. El intérprete ignora estos caracteres durante la ejecución.

```python
# Mucho más legible que 14000000000
presupuesto = 14_000_000_000 
referencia = 14000000000

print(presupuesto == referencia)
# Salida: True
```

***

### <mark style="color:yellow;">2. Números Decimales (</mark><mark style="color:yellow;">`float`</mark><mark style="color:yellow;">)</mark>

Cualquier número que contenga un punto decimal se instancia automáticamente como un objeto de la clase `float`.

```python
print(0.1 + 0.1)
# Salida: 0.2
```

#### <mark style="color:$danger;">Precisión de Punto Flotante (IEEE 754)</mark>

Al trabajar con decimales, es común encontrar resultados inesperados como el siguiente:

```python
print(0.2 + 0.1)
# Salida esperada: 0.3
# Salida real: 0.30000000000000004
```

**Explicación Técnica:** Esto no es un error de Python, sino una limitación del hardware. Las computadoras almacenan números en sistema binario (0 y 1) siguiendo el estándar **IEEE 754**. Fracciones simples en decimal como `0.1` o `0.2` son periódicas infinitas en binario (similar a 1/3 en decimal), lo que obliga a la computadora a guardar una aproximación, generando micro-errores de precisión.

#### <mark style="color:$danger;">Estrategias de Manejo</mark>

Dependiendo del contexto, existen tres formas de abordar este comportamiento:

1.  <mark style="color:$warning;">**Visualización (Redondeo):**</mark> Si el objetivo es mostrar el dato al usuario, usa `round()`.

    ```python
    resultado = 0.2 + 0.1
    print(round(resultado, 2)) # Redondea a 2 decimales
    # Salida: 0.3
    ```
2.  <mark style="color:$warning;">**Lógica (Tolerancia/Epsilon):**</mark> Para comparar floats, nunca uses `==`. Verifica si la diferencia es insignificante.

    ```python
    res = 0.2 + 0.1
    esperado = 0.3

    # Incorrecto
    print(res == esperado) # False

    # Correcto: ¿Es la diferencia menor a una tolerancia diminuta?
    print(abs(res - esperado) < 1e-9) # True
    ```
3.  <mark style="color:$warning;">**Precisión Crítica (Decimal):**</mark> Para software financiero o científico, usa el módulo `decimal`.

    ```python
    from decimal import Decimal
    # Importante: Pasar los números como strings para preservar exactitud
    print(Decimal('0.2') + Decimal('0.1'))
    # Salida: 0.3
    ```

***

### <mark style="color:yellow;">3. Coerción de Tipos y División</mark>

Python es un lenguaje flexible en operaciones mixtas.

#### <mark style="color:$danger;">Promoción Automática</mark>

Si operas un `int` con un `float`, Python convierte automáticamente el entero a flotante para no perder precisión.

```python
print(1 + 2.0)   # Resultado: 3.0 (float)
```

#### <mark style="color:$danger;">Comportamiento de la División (</mark><mark style="color:$danger;">`/`</mark><mark style="color:$danger;">)</mark>

En Python 3, el operador de división estándar (`/`) **siempre devuelve un float**, incluso si la división es exacta.

```python
print(4 / 2)
# Salida: 2.0
print(type(4 / 2))
# Salida: <class 'float'>
```

Esto garantiza consistencia en los resultados matemáticos, evitando errores antiguos (comunes en Python 2) donde `3 / 2` daba `1` en lugar de `1.5`.
