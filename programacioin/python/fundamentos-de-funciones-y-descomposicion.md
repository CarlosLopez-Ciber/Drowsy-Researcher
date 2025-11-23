# Fundamentos de Funciones y Descomposición

### <mark style="color:yellow;">1. Concepto de Descomposición Funcional</mark>

En el desarrollo de software, las funciones no son solo una herramienta de sintaxis, sino una estrategia de arquitectura. La **descomposición funcional** es la técnica de dividir un problema complejo en subproblemas más pequeños, abordables y aislados.

#### <mark style="color:$danger;">Ventajas Clave</mark>

1. **Reutilización:** Evita la repetición de lógica (principio DRY: _Don't Repeat Yourself_). Si un fragmento se usa en múltiples lugares, debe ser una función.
2. **Mantenimiento:** Es más fácil depurar una función pequeña y específica que un script monolítico de 500 líneas.
3. **Abstracción:** Permite pensar en "qué hace" el código (ej. `calcular_impuesto()`) sin preocuparse constantemente de "cómo lo hace".

#### <mark style="color:$danger;">Ejemplo de Arquitectura</mark>

Imagina una aplicación de facturación. En lugar de un solo bloque de código, se estructura así:

```python
# Arquitectura Modular
def obtener_datos_cliente():
    # Lógica de entrada
    pass

def calcular_total(productos):
    # Lógica de cálculo
    pass

def generar_factura():
    # Lógica de orquestación
    cliente = obtener_datos_cliente()
    total = calcular_total(...)
    print(f"Factura para {cliente}: {total}")
```

***

### <mark style="color:yellow;">2. Tipos de Funciones en Python</mark>

Es vital distinguir entre las herramientas que Python te da y las que tú construyes.

#### <mark style="color:$danger;">A. Funciones Integradas (Built-in)</mark>

Son parte del núcleo del lenguaje. Están optimizadas en C y disponibles inmediatamente sin importar nada.

|                 |               | Built-in Functions |                |                  |
| --------------- | ------------- | ------------------ | -------------- | ---------------- |
| `abs()`         | `delattr()`   | `hash()`           | `memoryview()` | `set()`          |
| `all()`         | `dict()`      | `help()`           | `min()`        | `setattr()`      |
| `any()`         | `dir()`       | `hex()`            | `next()`       | `slice()`        |
| `ascii()`       | `divmod()`    | `id()`             | `object()`     | `sorted()`       |
| `bin()`         | `enumerate()` | `input()`          | `oct()`        | `staticmethod()` |
| `bool()`        | `eval()`      | `int()`            | `open()`       | `str()`          |
| `breakpoint()`  | `exec()`      | `isinstance()`     | `ord()`        | `sum()`          |
| `bytearray()`   | `filter()`    | `issubclass()`     | `pow()`        | `super()`        |
| `bytes()`       | `float()`     | `iter()`           | `print()`      | `tuple()`        |
| `callable()`    | `format()`    | `len()`            | `property()`   | `type()`         |
| `chr()`         | `frozenset()` | `list()`           | `range()`      | `vars()`         |
| `classmethod()` | `getattr()`   | `locals()`         | `repr()`       | `zip()`          |
| `compile()`     | `globals()`   | `map()`            | `reversed()`   | `__import__()`   |
| `complex()`     | `hasattr()`   | `max()`            | `round()`      |                  |

* Referencia: [Documentación Oficial](https://docs.python.org/es/3.14/library/functions.html).

#### <mark style="color:$danger;">B. Funciones Definidas por el Usuario</mark>

Son las que creas para encapsular tu propia lógica de negocio.

* Sintaxis: Utilizan la palabra reservada `def`.

```python
def saludar(nombre):
    print(f"Hola, {nombre}")
```

***

### <mark style="color:yellow;">3. Flujo de Ejecución Interno</mark>

Comprender cómo Python gestiona las llamadas a funciones evita errores de lógica. El proceso no es lineal, sino que implica saltos en el puntero de ejecución.

1. **Invocación:** Python encuentra `mi_funcion()`.
2. **Suspensión:** Detiene la ejecución en la línea actual.
3. **Salto:** El control pasa a la primera línea del cuerpo de la función definida.
4. **Ejecución:** Se corre el código interno de la función.
5. **Retorno:** Al terminar (o encontrar un `return`), Python regresa exactamente al punto donde se detuvo en el paso 2.

***

### <mark style="color:yellow;">4. Reglas de Definición</mark>

Para evitar errores comunes (`NameError`, `SyntaxError`), sigue estas reglas estrictas:

1.  **Definir antes de invocar:** Python es interpretado. No puedes llamar a una función en la línea 5 si la defines en la línea 10.<br>

    ```python
    # Llama a la función suma
    suma(5, 5)

    # Se define la función suma
    def suma(a, b): return a + b

    # Salida: SyntaxError
    ```
2.  **Espacio de Nombres:** No uses nombres de funciones existentes para variables.

    ```python
    # ERROR DE PRINCIPIANTE
    def suma(a, b): return a + b

    suma = 10  # Has destruido la función 'suma', ahora es un entero.
    suma(5, 5) # TypeError: 'int' object is not callable
    ```
3. **Orden en el archivo:** Aunque deben definirse antes de usarse, las funciones pueden estar en cualquier orden entre ellas, siempre que la llamada principal ocurra al final.
