# Funciones - Parámetros y Argumentos

### <mark style="color:yellow;">1. Distinción Técnica: Parámetro vs. Argumento</mark>

Aunque coloquialmente se usan como sinónimos, en ingeniería de software es vital distinguir entre ambos conceptos para entender la documentación y los errores de ejecución.

* **Parámetro:** Es la variable declarada **dentro del paréntesis** en la definición de la función. Su alcance es estrictamente local; existe solo dentro de la función.
* **Argumento:** Es el valor real (dato) que se envía a la función desde el código exterior al momento de invocarla.

**Sintaxis Básica:**

```python
# 'mensaje' es el PARÁMETRO
def mostrar(mensaje):
    print(mensaje)

# "Hola" es el ARGUMENTO
mostrar("Hola")
```

Si se omite un argumento requerido para un parámetro definido, Python detendrá la ejecución con un `TypeError`.

***

### <mark style="color:yellow;">2. Estrategias de Paso de Argumentos</mark>

Python ofrece flexibilidad en cómo los argumentos se asignan a los parámetros.

#### <mark style="color:$danger;">A. Argumentos Posicionales</mark>

Es el método estándar. Python asigna los valores basándose estrictamente en el **orden de llegada**. El primer argumento se asigna al primer parámetro, el segundo al segundo, y así sucesivamente.

Importancia del Orden:

Dado que la asignación es ciega (basada en posición), cambiar el orden altera drásticamente la lógica.

```python
def configurar_servidor(ip, puerto, protocolo):
    print(f"Conectando a {ip}:{puerto} vía {protocolo}")

# Orden Correcto
configurar_servidor("192.168.1.10", 8080, "TCP")
# Salida: Conectando a 192.168.1.10:8080 vía TCP

# Orden Incorrecto (Error Lógico)
configurar_servidor(8080, "TCP", "192.168.1.10")
# Salida: Conectando a 8080:TCP vía 192.168.1.10 (Sin sentido)
```

#### <mark style="color:$danger;">B. Argumentos por Palabra Clave (Keyword Arguments)</mark>

Permite asignar valores explícitamente usando el nombre del parámetro (`nombre=valor`). En esta modalidad, **la posición es irrelevante**, lo que aumenta la legibilidad y reduce errores en funciones con múltiples parámetros.

```python
def introduccion(nombre, apellido):
    print(f"{nombre} {apellido}")

# El orden no importa
introduccion(apellido="Skywalker", nombre="Luke")
# Salida: Luke Skywalker
```

**Restricción:** El nombre usado en la llamada debe coincidir exactamente con el nombre del parámetro definido. Usar un nombre inexistente (ej. `apellidos` en lugar de `apellido`) generará un `TypeError`.

***

### <mark style="color:yellow;">3. Combinación de Estrategias</mark>

Es posible y común mezclar ambos métodos en una sola invocación. Sin embargo, existe una **Regla de Oro de Sintaxis**:

> **Los argumentos posicionales deben preceder siempre a los argumentos por palabra clave.**.

Si colocas un argumento posicional después de uno con nombre, Python no sabrá a qué posición corresponde, generando un error de sintaxis.

**Análisis de Casos:**

```python
def suma(a, b, c):
    return a + b + c

# ✅ VÁLIDO: Posicionales primero, luego keywords
suma(1, c=3, b=2) 
# a=1 (posicional), b=2 (keyword), c=3 (keyword)

# ❌ INVÁLIDO: Posicional después de keyword
# suma(a=1, 2, 3)
# SyntaxError: positional argument follows keyword argument

# ❌ INVÁLIDO: Duplicidad de asignación
# suma(1, a=2, b=3)
# TypeError: got multiple values for argument 'a' (1 y 2)
```

***

### <mark style="color:yellow;">4. Flexibilidad: Valores por Defecto</mark>

Para hacer que un argumento sea **opcional**, se puede asignar un valor por defecto en la definición de la función. Si el invocador no proporciona un valor, se usa el predeterminado.

#### <mark style="color:$danger;">Regla de Definición</mark>

Al igual que en la invocación, en la definición **los parámetros con valores por defecto deben ir al final**, después de los parámetros obligatorios.

```python
# ✅ Correcto
def conexion(host, puerto=80, timeout=30):
    pass

# ❌ Incorrecto (SyntaxError)
# def conexion(puerto=80, host):
#     pass
```

#### <mark style="color:$danger;">Comportamiento en Ejecución</mark>

Python evalúa los valores por defecto **una sola vez** al momento de definir la función, no cada vez que se llama. Esto es eficiente, pero requiere precaución con tipos mutables (listas/diccionarios).

**Ejemplo de Uso:**

```python
def saludar(nombre="Visitante"):
    print(f"Hola, {nombre}")

saludar("Ana") # Usa el argumento: "Hola, Ana"
saludar()      # Usa el defecto:   "Hola, Visitante"
```
