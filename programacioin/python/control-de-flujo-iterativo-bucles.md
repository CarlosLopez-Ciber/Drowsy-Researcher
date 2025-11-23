# Control de Flujo Iterativo: Bucles

En programación, una de las tareas más comunes es la repetición de una tarea. Ya sea procesar mil filas de una base de datos, enviar correos a una lista de usuarios o esperar a que un servidor responda, necesitamos estructuras que repitan bloques de código. Estas estructuras se denominan **Bucles** (o Ciclos).

Python ofrece dos primitivas para la iteración:

1. **`for`**: Para iterar sobre una secuencia de elementos conocida (definida).
2. **`while`**: Para iterar mientras se cumpla una condición lógica (indefinida).

***

### <mark style="color:yellow;">1. El Bucle</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">`for`</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">(Iterador)</mark>

A diferencia de otros lenguajes (como C o Java) donde el `for` se basa en un contador numérico (`i=0; i<10; i++`), el `for` en Python actúa como un **iterador**. Su función es recorrer los elementos de una colección (lista, tupla, string, diccionario) uno por uno.

#### Sintaxis

```python
for variable_temporal in coleccion:
    # Bloque de código a repetir
    # La 'variable_temporal' toma el valor del elemento actual
```

#### Ejemplo: Recorriendo una Lista

```python
tecnologias = ["Python", "Docker", "Linux"]

for tech in tecnologias:
    print(f"Aprendiendo: {tech}")
```

**Salida:**

```
Aprendiendo: Python
Aprendiendo: Docker
Aprendiendo: Linux
```

#### Generación de Secuencias: `range()`

Para iterar un número específico de veces, no creamos una lista `[0, 1, 2...]` manualmente. Usamos la función `range()`.

* `range(stop)`: De 0 hasta stop-1.
* `range(start, stop)`: De start hasta stop-1.
* `range(start, stop, step)`: Saltando de step en step.

```python
# Imprimir números del 0 al 4
for i in range(5):
    print(f"Iteración {i}")
```

***

### <mark style="color:yellow;">2. El Bucle</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">`while`</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">(Condicional)</mark>

El bucle `while` repite el bloque de código **mientras** una condición booleana sea `True`. Es ideal cuando no sabemos de antemano cuántas veces necesitamos repetir la acción (por ejemplo, esperar input del usuario).

#### Sintaxis

```python
while condicion:
    # Bloque de código
    # Importante: Algo debe cambiar la condición eventualmente
```

#### Ejemplo: Cuenta Regresiva

```python
contador = 5

while contador > 0:
    print(f"Despegue en {contador}...")
    contador -= 1  # Modificamos la variable de control

print("¡Despegue!")
```

#### El Peligro: Bucles Infinitos

Si la condición del `while` nunca se vuelve `False`, el programa se ejecutará eternamente, consumiendo CPU hasta que el sistema lo detenga o el usuario fuerce el cierre.

```python
# EJEMPLO DE BUCLE INFINITO (No ejecutar)
# while True:
#     print("Esto nunca termina")
```

_Nota: Si caes en uno, usa `Ctrl + C` en la terminal para interrumpirlo._

***

### <mark style="color:yellow;">3. Control de Interrupción (</mark><mark style="color:yellow;">`break`</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">y</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">`continue`</mark><mark style="color:yellow;">)</mark>

Python permite alterar el flujo natural del ciclo desde dentro.

#### <mark style="color:$danger;">`break`</mark> <mark style="color:$danger;"></mark><mark style="color:$danger;">(Romper)</mark>

Termina el bucle inmediatamente, saltando a la primera línea de código fuera del ciclo. Se usa comúnmente para búsquedas (parar cuando encuentras lo que buscas).

```python
ciudades = ["Lima", "Bogotá", "Santiago", "Quito"]

for ciudad in ciudades:
    if ciudad == "Santiago":
        print("Ciudad encontrada. Deteniendo búsqueda.")
        break  # Sale del for
    print(f"Verificando {ciudad}...")
```

#### <mark style="color:$danger;">`continue`</mark> <mark style="color:$danger;"></mark><mark style="color:$danger;">(Saltar)</mark>

Detiene la iteración **actual** y salta inmediatamente a la siguiente, ignorando el resto del código en ese ciclo específico.

```python
# Imprimir solo números impares
for i in range(6):
    if i % 2 == 0:
        continue  # Si es par, salta a la siguiente vuelta
    print(f"Número impar: {i}")
```

***

### <mark style="color:yellow;">4.</mark>  <mark style="color:yellow;"></mark><mark style="color:yellow;">`else`</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">en Bucles</mark>

Python tiene una característica única: los bucles `for` y `while` pueden tener un bloque `else`.

**¿Cuándo se ejecuta el else?** Se ejecuta **solo si el bucle terminó naturalmente** (agotó la lista o la condición while fue falsa). **NO** se ejecuta si el bucle fue interrumpido por un break.

Esto es muy útil para búsquedas:

```python
busqueda = 50
numeros = [10, 20, 30]

for n in numeros:
    if n == busqueda:
        print("Número encontrado")
        break
else:
    # Solo se ejecuta si el 'break' NO se tocó
    print("El número no está en la lista")
```
