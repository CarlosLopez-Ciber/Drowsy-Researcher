# Operadores Aritméticos

Los operadores aritméticos son los símbolos reservados que permiten realizar operaciones matemáticas fundamentales. En Python, estos operadores poseen una característica importante: el **polimorfismo** (o sobrecarga de operadores). Esto significa que un mismo símbolo (como `+`) puede comportarse de manera diferente según el tipo de dato que esté manipulando.

### <mark style="color:yellow;">Tabla de Referencia</mark>

| **Operador** | **Nombre**      | **Descripción**                              | **Ejemplo** |
| ------------ | --------------- | -------------------------------------------- | ----------- |
| `+`          | Suma            | Suma aritmética o concatenación.             | `a + b`     |
| `-`          | Resta           | Sustracción aritmética.                      | `a - b`     |
| `*`          | Multiplicación  | Producto o repetición de secuencias.         | `a * b`     |
| `/`          | División Real   | División estándar. Siempre devuelve `float`. | `a / b`     |
| `//`         | División Entera | División que trunca los decimales (piso).    | `a // b`    |
| `%`          | Módulo          | Devuelve el residuo de la división.          | `a % b`     |
| `**`         | Exponenciación  | Eleva un número a una potencia.              | `a ** b`    |
| `-` (unario) | Negación        | Invierte el signo de un número.              | `-a`        |

***

### <mark style="color:yellow;">1. Operadores Básicos:</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">`+`</mark><mark style="color:yellow;">,</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">`-`</mark><mark style="color:yellow;">,</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">`*`</mark>

#### <mark style="color:$danger;">Contexto Numérico (</mark><mark style="color:$danger;">`int`</mark> <mark style="color:$danger;"></mark><mark style="color:$danger;">y</mark> <mark style="color:$danger;"></mark><mark style="color:$danger;">`float`</mark><mark style="color:$danger;">)</mark>

Con números, estos operadores funcionan según las reglas matemáticas estándar.

```python
x = 10
y = 5

print(x + y)  # 15
print(x - y)  # 5
print(x * y)  # 50
```

#### <mark style="color:$danger;">Contexto de Cadenas (</mark><mark style="color:$danger;">`str`</mark><mark style="color:$danger;">)</mark>

Aquí se aplica la sobrecarga de operadores:

* **Suma (`+`):** Realiza una **concatenación** (unión de cadenas).
* **Multiplicación (`*`):** Realiza una **repetición** (debe ser `str * int`).
* **Resta (`-`):** No está definida para cadenas y genera un `TypeError`.

```python
texto_a = "Hola"
texto_b = "Mundo"

# Concatenación
print(texto_a + " " + texto_b)
# Salida: Hola Mundo

# Repetición (Muy útil para separadores visuales)
print("-" * 10)
# Salida: ----------
```

***

### <mark style="color:yellow;">2. Tipos de División:</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">`/`</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">vs</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">`//`</mark>

Es crítico distinguir entre los dos tipos de división en Python 3.

#### <mark style="color:$danger;">División Verdadera (</mark><mark style="color:$danger;">`/`</mark><mark style="color:$danger;">)</mark>

El operador de barra simple siempre realiza una división matemática completa.

Regla: El resultado siempre es de tipo float, incluso si la división es exacta.

```python
print(10 / 2)
# Salida: 5.0 (float)

print(10 / 3)
# Salida: 3.3333333333333335
```

#### <mark style="color:$danger;">División Entera (</mark><mark style="color:$danger;">`//`</mark><mark style="color:$danger;">)</mark>

El operador de doble barra, también conocido como _Floor Division_, divide los números y **trunca** la parte decimal, redondeando hacia el entero inferior más cercano.

```python
print(10 // 3)
# Salida: 3 (Se descarta el .333...)

print(10 // 7)
# Salida: 1
```

***

### <mark style="color:yellow;">3. Aritmética Avanzada: Módulo y Potencia</mark>

#### <mark style="color:$danger;">Módulo (</mark><mark style="color:$danger;">`%`</mark><mark style="color:$danger;">)</mark>

El operador de módulo devuelve el **residuo** o resto de una división entera. No devuelve el cociente.

Este operador es fundamental en algoritmos para determinar ciclos o paridad.

**Caso de Uso: Paridad (Pares e Impares)**

* Si un número dividido por 2 tiene residuo 0, es par.
* Si el residuo es 1, es impar.

```python
numero = 10

# 10 dividido por 7 es 1, y sobran 3
print(10 % 7) 
# Salida: 3

# Verificación de paridad
print(10 % 2) # Salida: 0 (Es par)
print(11 % 2) # Salida: 1 (Es impar)
```

#### <mark style="color:$danger;">Exponenciación (</mark><mark style="color:$danger;">`**`</mark><mark style="color:$danger;">)</mark>

Eleva el operando izquierdo a la potencia del derecho ($a^b$). Es equivalente a la función `pow(a, b)` pero más conciso.

```python
base = 10
exponente = 3

print(base ** exponente)
# Salida: 1000
```

***

### <mark style="color:yellow;">4. Operadores Unarios</mark>

Los operadores unarios actúan sobre un solo operando, colocado inmediatamente a su derecha.

* **Negativo (`-`):** Invierte el signo del valor numérico.
* **Positivo (`+`):** Indica explícitamente que el valor es positivo (generalmente redundante y poco usado, pero existe por simetría matemática).

```python
valor = 10
negativo = -valor

print(negativo)
# Salida: -10
```

Nota: Estos operadores no son aplicables a cadenas de texto. Intentar `-"Texto"` resultará en un `TypeError`.
