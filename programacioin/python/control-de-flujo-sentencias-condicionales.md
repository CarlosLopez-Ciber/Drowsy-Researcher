# Control de Flujo: Sentencias Condicionales

Hasta ahora, los scripts se han ejecutado secuencialmente, línea por línea desde arriba hacia abajo. Las estructuras de control condicional rompen este flujo lineal, permitiendo que el programa tome decisiones.

Python utiliza la sentencia `if` (si) para evaluar si una condición es verdadera. Si lo es, ejecuta un bloque de código; de lo contrario, lo ignora o ejecuta un camino alternativo.

#### <mark style="color:$danger;">Anatomía de una Decisión</mark>

Analicemos un caso práctico: iterar una lista de autos y formatear sus nombres. La regla de negocio es: "Todos los nombres llevan mayúscula inicial, excepto 'bmw', que debe ser todo mayúsculas".

```python
autos = ['audi', 'bmw', 'subaru', 'toyota']

for auto in autos:
    # Inicio de la estructura condicional
    if auto == 'bmw':
        print(auto.upper())  # Acción A: Si es BMW
    else:
        print(auto.title())  # Acción B: Si NO es BMW
```

**Salida:**

```
AudiBMWSubaruToyota
```

***

### <mark style="color:yellow;">1. Pruebas Condicionales</mark>

El núcleo de una sentencia `if` es la **Expresión Booleana**. Python evalúa esta expresión y, si el resultado es `True`, permite el acceso al bloque de código.

#### <mark style="color:$danger;">Igualdad y Desigualdad</mark>

* `==` (Igualdad): Compara si dos valores son idénticos.<br>
* `!=` (Desigualdad): Compara si dos valores son diferentes.<br>

**Nota sobre Strings:** Las comparaciones son sensibles a mayúsculas (_case-sensitive_). `'Audi' == 'audi'` devuelve `False`. Para comparaciones insensibles, se recomienda normalizar el texto con `.lower()` antes de comparar.

```python
# Normalización para comparación segura
car = 'Audi'
if car.lower() == 'audi':
    print("Coincidencia encontrada")
```

#### <mark style="color:$danger;">Comparaciones Numéricas</mark>

Se aplican los operadores matemáticos estándar:

```python
edad = 19
print(edad >= 18)  # True (Mayor o igual)
print(edad < 21)   # True (Menor estricto)
print(edad != 0)   # True (Diferente de)
```

#### <mark style="color:$danger;">Operadores Lógicos (</mark><mark style="color:$danger;">`and`</mark><mark style="color:$danger;">,</mark> <mark style="color:$danger;"></mark><mark style="color:$danger;">`or`</mark><mark style="color:$danger;">)</mark>

Permiten combinar múltiples condiciones en una sola evaluación.

* **`and`**: Ambas condiciones deben ser `True`.<br>
* **`or`**: Al menos una condición debe ser `True`.

```python
edad_1 = 22
edad_2 = 18

# Ambas deben cumplirse
if (edad_1 >= 21) and (edad_2 >= 21):
    print("Ambos son mayores de 21") # No se ejecuta
```

#### <mark style="color:$danger;">Comprobación en Listas (</mark><mark style="color:$danger;">`in`</mark><mark style="color:$danger;">,</mark> <mark style="color:$danger;"></mark><mark style="color:$danger;">`not in`</mark><mark style="color:$danger;">)</mark>

Esencial para validar si un elemento existe dentro de una colección antes de procesarlo.

```python
usuarios_baneados = ['andrew', 'carolina', 'david']
usuario_actual = 'marie'

if usuario_actual not in usuarios_baneados:
    print(f"{usuario_actual}, acceso permitido.")
```

***

### <mark style="color:yellow;">2. Estructuras Sintácticas</mark>

Python utiliza la **indentación** (sangría) para delimitar los bloques de código. Esto reemplaza las llaves `{}` usadas en otros lenguajes como C o Java.

#### <mark style="color:$danger;">A. Sentencia</mark> <mark style="color:$danger;"></mark><mark style="color:$danger;">`if`</mark> <mark style="color:$danger;"></mark><mark style="color:$danger;">Simple</mark>

Ejecuta una acción solo si la condición es verdadera.

```python
edad = 19
if edad >= 18:
    print("Eres mayor de edad.")
```

#### <mark style="color:$danger;">B. Sentencia</mark> <mark style="color:$danger;"></mark><mark style="color:$danger;">`if-else`</mark>

Define dos caminos mutuamente excluyentes: uno si la condición es `True` y otro si es `False`.

```python
edad = 17
if edad >= 18:
    print("Puedes votar.")
else:
    print("Demasiado joven para votar.")
```

#### <mark style="color:$danger;">C. Cadena</mark> <mark style="color:$danger;"></mark><mark style="color:$danger;">`if-elif-else`</mark>

Evalúa múltiples condiciones en orden secuencial. **Importante:** Python ejecuta solo el primer bloque cuya condición sea verdadera y omite el resto.

_Ejemplo: Tarifas de parque de diversiones._

```python
edad = 12

if edad < 4:
    precio = 0
elif edad < 18:
    precio = 25
elif edad < 65:
    precio = 40
else:
    precio = 20  # Tarifa para mayores de 65

print(f"Tu costo de entrada es ${precio}.")
```

**Optimización:** Observa cómo establecemos una variable `precio` en lugar de imprimir en cada bloque. Esto hace el código más mantenible y sigue el principio DRY (Don't Repeat Yourself).

***

### <mark style="color:yellow;">3. Patrones Avanzados y Buenas Prácticas</mark>

#### <mark style="color:$danger;">El</mark> <mark style="color:$danger;"></mark><mark style="color:$danger;">`else`</mark> <mark style="color:$danger;"></mark><mark style="color:$danger;">es Opcional</mark>

No es obligatorio cerrar una cadena `elif` con un `else`. De hecho, si se espera una condición específica final, es más seguro usar un `elif` explícito para evitar procesar datos inválidos o maliciosos que caerían en un `else` genérico.

#### <mark style="color:$danger;">Múltiples</mark> <mark style="color:$danger;"></mark><mark style="color:$danger;">`if`</mark> <mark style="color:$danger;"></mark><mark style="color:$danger;">vs</mark> <mark style="color:$danger;"></mark><mark style="color:$danger;">`elif`</mark>

Esta distinción es crítica para la lógica del programa.

* **Usar `if-elif`:** Cuando las condiciones son excluyentes (si pasa una, no pueden pasar las otras). _Ejemplo: Tu edad._<br>
* **Usar múltiples `if`:** Cuando más de una condición puede ser verdadera simultáneamente. _Ejemplo: Ingredientes de una pizza._

```python
# INCORRECTO para ingredientes (usando elif)
# Si tiene champiñones, Python dejará de buscar y no añadirá el queso extra.
if 'champiñones' in pedido:
    agregar('champiñones')
elif 'queso extra' in pedido:
    agregar('queso_extra') 

# CORRECTO (usando if independientes)
if 'champiñones' in pedido:
    agregar('champiñones')
if 'queso extra' in pedido:
    agregar('queso_extra')
```

#### <mark style="color:$danger;">Listas Vacías como Booleanos</mark>

En Python, las listas vacías se evalúan como `False` y las listas con contenido como `True`. Esto permite verificar si hay datos antes de iniciar un bucle.

```python
pedido = []

if pedido: # Equivale a: if len(pedido) > 0:
    for item in pedido:
        print(f"Añadiendo {item}")
else:
    print("¿Seguro que quieres una pizza simple?")
```

#### <mark style="color:$danger;">Validación Cruzada de Listas</mark>

Un patrón común es procesar una lista de solicitudes contra una lista de disponibilidades.

```python
disponibles = ['champiñones', 'aceitunas', 'pepperoni']
solicitados = ['champiñones', 'papas fritas', 'pepperoni']

for item in solicitados:
    if item in disponibles:
        print(f"Añadiendo {item}.")
    else:
        print(f"Lo sentimos, no tenemos {item}.")
```

**Salida:**

```
Añadiendo champiñones.Lo sentimos, no tenemos papas fritas.Añadiendo pepperoni.
```
