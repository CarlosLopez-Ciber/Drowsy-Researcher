# Lógica Booleana

Las condiciones simples (`edad > 18`) son la base de la toma de decisiones, pero el mundo real rara vez es tan sencillo. Frecuentemente necesitamos evaluar múltiples criterios simultáneamente: _"¿El usuario es administrador Y tiene la sesión activa?"_ o _"¿El archivo existe O tenemos permisos de creación?"_.

Para modelar estas reglas complejas, Python utiliza los **operadores lógicos**. Estos permiten combinar múltiples expresiones booleanas en un único resultado de verdad.

### <mark style="color:yellow;">Tabla de Referencia</mark>

| **Operador** | **Nombre Técnico** | **Comportamiento**                                                 |
| ------------ | ------------------ | ------------------------------------------------------------------ |
| **`not`**    | Negación (Unario)  | Invierte el valor. `True` ➝ `False`.                               |
| **`and`**    | Conjunción         | Devuelve `True` solo si **todos** los operandos son verdaderos.    |
| **`or`**     | Disyunción         | Devuelve `True` si **al menos uno** de los operandos es verdadero. |

***

### <mark style="color:yellow;">1. El Operador</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">`not`</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">(Negación)</mark>

Es un operador **unario**, lo que significa que actúa sobre un solo operando situado a su derecha. Su función es invertir el valor de verdad.

```python
conectado = False

if not conectado:
    print("El usuario está desconectado.")
    # Salida: El usuario está desconectado.
```

**Tabla de Verdad:**

| **A**   | **not A** |
| ------- | --------- |
| `True`  | `False`   |
| `False` | `True`    |

***

### <mark style="color:yellow;">2. El Operador</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">`and`</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">(Conjunción)</mark>

Evalúa si **ambas** condiciones se cumplen simultáneamente. Es el operador más estricto; basta con que una condición falle para que el resultado global sea falso.

```python
usuario = "Admin"
password_correcta = True

if (usuario == "Admin") and password_correcta:
    print("Acceso al panel de control concedido.")
```

**Tabla de Verdad:**

| **A**   | **B**   | **A and B** |
| ------- | ------- | ----------- |
| `True`  | `True`  | `True`      |
| `True`  | `False` | `False`     |
| `False` | `True`  | `False`     |
| `False` | `False` | `False`     |

***

### <mark style="color:yellow;">3. El Operador</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">`or`</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">(Disyunción)</mark>

Evalúa si **alguna** de las condiciones se cumple. Es un operador inclusivo: devuelve verdadero si A es verdadero, si B es verdadero, o si ambos lo son.

```python
tiene_entrada = False
es_vip = True

if tiene_entrada or es_vip:
    print("Puede ingresar al evento.")
```

**Tabla de Verdad:**

| **A**   | **B**   | **A or B** |
| ------- | ------- | ---------- |
| `True`  | `True`  | `True`     |
| `True`  | `False` | `True`     |
| `False` | `True`  | `True`     |
| `False` | `False` | `False`    |

***

### <mark style="color:yellow;">4. Concepto Avanzado: Evaluación de Cortocircuito</mark>

Python utiliza una estrategia de optimización llamada **Short-Circuit Evaluation** (Evaluación Perezosa). Esto significa que el intérprete deja de evaluar la expresión tan pronto como conoce el resultado final.

#### <mark style="color:$danger;">Cortocircuito en</mark> <mark style="color:$danger;"></mark><mark style="color:$danger;">`and`</mark>

Si el primer valor es `False`, Python **no evalúa el segundo**, porque ya sabe que el resultado total será `False` pase lo que pase.

```python
def funcion_pesada():
    print("Ejecutando cálculo complejo...")
    return True

# Como la primera condición es False, funcion_pesada() NUNCA se ejecuta.
if False and funcion_pesada():
    print("Esto no se imprime")
```

#### <mark style="color:$danger;">Cortocircuito en</mark> <mark style="color:$danger;"></mark><mark style="color:$danger;">`or`</mark>

Si el primer valor es `True`, Python **no evalúa el segundo**, porque ya sabe que el resultado total será `True`.

```python
# Como la primera condición es True, funcion_pesada() NUNCA se ejecuta.
if True or funcion_pesada():
    print("Entramos al if")
```

> **Uso Práctico:** Esto es vital para evitar errores en tiempo de ejecución. Por ejemplo, verificar si una variable es `None` antes de llamar a un método suyo.

```
usuario = None

# Seguro: Python ve que usuario es None (False en booleano) y se detiene.
# No intenta ejecutar .es_activo(), evitando un AttributeError.
if usuario and usuario.es_activo():
    print("Activo")
```

***

### <mark style="color:yellow;">5. Jerarquía de Operaciones (Precedencia)</mark>

Cuando combinas múltiples operadores en una sola línea, Python sigue un orden estricto de evaluación (similar a la multiplicación antes que la suma en matemáticas):

1. **`not`** (Se evalúa primero)
2. **`and`**
3. **`or`** (Se evalúa al final)

<mark style="color:$danger;">Ejemplo de ambigüedad:</mark>

```python
# ¿Se interpreta como (True or False) and False? -> False
# ¿O se interpreta como True or (False and False)? -> True
resultado = True or False and False 
```

Debido a la precedencia (`and` gana a `or`), Python lo interpreta como: `True or (False and False)`, lo que da **`True`**.

Buenas Prácticas:

Aunque conozcas la precedencia, usa siempre paréntesis () para agrupar condiciones complejas. Esto elimina la ambigüedad para los humanos que leen tu código.

```python
# Código legible y seguro
if (edad > 18) and (tiene_dinero or tiene_invitacion):
    print("Bienvenido")
```

