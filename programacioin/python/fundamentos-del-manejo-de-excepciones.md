# Fundamentos del Manejo de Excepciones

### <mark style="color:yellow;">La Filosofía del Error</mark>

En el desarrollo de software, asumir que todo funcionará perfectamente es una utopía. La robustez de un programa no se mide por la ausencia de errores, sino por su capacidad para **anticiparlos, identificarlos y manejarlos** sin detenerse abruptamente.

> “Errar es humano. Pero ignorar los errores es una negligencia técnica.”

#### <mark style="color:$danger;">Clasificación de Errores</mark>

Antes de escribir código, es vital distinguir a qué nos enfrentamos:

1. **Errores en Datos de Entrada:** Ocurren cuando el usuario o una fuente externa provee información inválida (ej. introducir texto cuando se espera un número). No son culpa del programador, pero es su responsabilidad gestionarlos.
2. **Errores Lógicos (Bugs):** Son fallos en el diseño del código (ej. una fórmula matemática incorrecta). Estos no siempre lanzan alertas, pero generan resultados erróneos y son los más peligrosos.

***

### <mark style="color:yellow;">1. La Estructura</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">`try`</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">-</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">`except`</mark>

Para evitar que un error detenga el programa (crash), Python ofrece el bloque de control `try-except`.

#### <mark style="color:$danger;">Mecánica de Ejecución</mark>

* **Bloque `try`:** Contiene el código "riesgoso" que podría fallar. Python intenta ejecutarlo línea por línea.
* **Bloque `except`:** Contiene el código de "rescate". Solo se ejecuta si ocurre un error dentro del `try`. Si no hay error, este bloque se ignora completamente.

#### Ejemplo Práctico: División por Cero

```python
try:
    # Intentamos convertir y dividir
    x = int(input("Ingrese un número divisor para 10: "))
    resultado = 10 / x
    print(f"Resultado: {resultado}")

except ZeroDivisionError:
    # Este código solo corre si x es 0
    print("Error: No es posible dividir por cero.")

except ValueError:
    # Este código solo corre si x no es un número (ej. 'hola')
    print("Error: Debe ingresar un número entero válido.")
```

En este ejemplo, el programa no se cierra abruptamente con un mensaje rojo en consola, sino que informa al usuario del problema y podría continuar su ejecución o volver a pedir el dato.

***

### <mark style="color:yellow;">2. Manejo de Múltiples Excepciones</mark>

Un mismo bloque de código puede fallar por múltiples razones. Python evalúa los bloques `except` en orden descendente y ejecuta **solo el primero que coincida** con el tipo de error encontrado.

#### <mark style="color:$danger;">Estrategia A: Manejo Individual (Recomendado)</mark>

Permite dar retroalimentación específica para cada error.

```python
try:
    valor = int(input("Ingrese un número: "))
    res = 10 / valor
except ValueError:
    print("Error de Tipo: Eso no es un número.")
except ZeroDivisionError:
    print("Error Matemático: No se puede dividir por 0.")
```

#### <mark style="color:$danger;">Estrategia B: Agrupación de Excepciones</mark>

Si la respuesta o solución es la misma para varios errores, se pueden agrupar en una tupla dentro de un solo `except`.

```python
try:
    valor = int(input("Ingrese un número: "))
    res = 10 / valor
except (ValueError, ZeroDivisionError):
    print("Operación inválida (Entrada incorrecta o división por cero).")
```

***

### <mark style="color:yellow;">3. Ventajas del Modelo de Excepciones</mark>

Implementar este patrón ofrece beneficios claros frente a la validación tradicional con `if/else`:

1. **Claridad:** Separa la lógica de negocio (el "camino feliz" dentro del `try`) de la lógica de gestión de errores (dentro del `except`).
2. **Protección:** Evita fallos críticos por situaciones externas (como un archivo no encontrado o falta de red).

#### <mark style="color:$danger;">Advertencia Profesional</mark>

El uso de `try-except` no sustituye la validación lógica. No se debe usar para controlar el flujo normal del programa, sino para gestionar situaciones excepcionales.

* **Incorrecto:** Usar `try` para abrir un archivo y `except` para todo lo demás.

```python
try:
    archivo = open("datos.txt", "r")
except:
    print("Algo salió mal...")
```

* **Correcto:** Usar `try` específicamente para capturar `FileNotFoundError` si el archivo no existe.

```python
try:
    archivo = open("datos.txt", "r")
except FileNotFoundError:
    print("Error: El archivo no fue encontrado.")
```
