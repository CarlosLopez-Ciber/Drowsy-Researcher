# Buenas Prácticas y Tipología de Errores

### <mark style="color:yellow;">1. La Excepción por Defecto (</mark><mark style="color:yellow;">`except`</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">genérico)</mark>

En ocasiones, es imposible anticipar _todos_ los errores posibles. Para evitar que el programa se detenga ante un fallo desconocido, Python permite el uso de un bloque `except` sin nombre específico.

#### <mark style="color:$danger;">Sintaxis y Jerarquía</mark>

Este bloque funciona como una red de seguridad final. **Regla de Oro:** Debe colocarse siempre al **final** de la cadena de excepciones. Si se coloca antes de una excepción específica, generará un `SyntaxError` porque la haría inaccesible.

```python
try:
    # Código riesgoso
    operacion = 10 / 0
except ZeroDivisionError:
    # Manejo específico
    print("División por cero.")
except:
    # Manejo genérico (Catch-All)
    print("Error inesperado no manejado anteriormente.")
```

#### <mark style="color:$danger;">El Riesgo de la Opacidad</mark>

Usar `except:` (vacío) se considera una práctica peligrosa en desarrollo profesional porque "traga" cualquier error sin dejar rastro, dificultando la depuración.

**Mejor Práctica: Capturar la excepción como objeto usando Exception.**

Esto atrapa cualquier error estándar pero permite inspeccionar el mensaje técnico.

```python
try:
    # Código...
    pass
except Exception as e:
    # Muestra QUÉ pasó sin detener el programa
    print(f"Se produjo un error inesperado: {e}")
```

***

### <mark style="color:yellow;">2. Diccionario de Excepciones Comunes</mark>

Python posee una jerarquía de clases para sus errores. Conocer las más frecuentes es vital para escribir bloques `except` precisos.

| **Excepción**           | **Descripción Técnica**                                                                                                                                | **Ejemplo de Causa**                                     |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------- |
| **`ZeroDivisionError`** | Operación matemática inválida por división entre cero. Afecta a `/`, `//` y `%`.                                                                       | `x = 5 / 0`                                              |
| **`ValueError`**        | El tipo de dato es correcto, pero el valor es inapropiado para la operación.                                                                           | `int("abc")` (No puede convertir letras a entero)        |
| **`TypeError`**         | Operación entre tipos incompatibles o índice inválido.                                                                                                 | `lista["1"]` (Índice debe ser int, no str) o `3 + "a"`   |
| **`AttributeError`**    | Intento de acceso a un método o atributo inexistente en el objeto.                                                                                     | `lista.no_existe()`                                      |
| **`SyntaxError`**       | Violación de la gramática del lenguaje. Se detecta antes de la ejecución (parsing). **No se debe manejar con try-except**, se debe corregir el código. | `eval("for i in range(5) print(i)")` (Faltan dos puntos) |

***

### <mark style="color:yellow;">3. El Fenómeno de los Errores Silenciados</mark>

Uno de los problemas más insidiosos en el manejo de excepciones es cuando el bloque `try` oculta errores de programación (bugs) porque el flujo de ejecución se interrumpe antes de llegar a ellos.

#### <mark style="color:$danger;">El "Bug" Fantasma</mark>

Analicemos este código con un error tipográfico intencional (`prin` en lugar de `print`):

```python
try:
    valor = int(input("Ingrese un número: "))
    resultado = 10 / valor
    # ERROR TIPOGRÁFICO AQUÍ ABAJO:
    prin(f"Resultado: {resultado}") 
except ZeroDivisionError:
    print("Error: División por cero.")
```

<mark style="color:$warning;">**Escenario A: Usuario ingresa**</mark><mark style="color:$warning;">**&#x20;**</mark><mark style="color:$warning;">**`0`**</mark>

1. Se ejecuta `int("0")`.
2. Se intenta `10 / 0`.
3. Se lanza `ZeroDivisionError`.
4. El flujo salta inmediatamente al `except`.
5. **Resultado:** El programa "funciona" correctamente y muestra el error de división. La línea con `prin` **nunca se ejecutó**, por lo que el bug permanece oculto.

<mark style="color:$warning;">**Escenario B: Usuario ingresa**</mark><mark style="color:$warning;">**&#x20;**</mark><mark style="color:$warning;">**`5`**</mark>

1. La división `10 / 5` es exitosa.
2. El flujo llega a `prin(...)`.
3. Python lanza un `NameError` (porque la función `prin` no existe).
4. Como no hay un `except NameError`, el programa colapsa (crash).

#### <mark style="color:$danger;">Solución Profesional</mark>

Para evitar que estos errores de sintaxis o nombres pasen desapercibidos hasta que sea demasiado tarde (producción), se recomienda:

1. Usar **Linters** (herramientas de análisis estático) en el editor de código para detectar `prin` antes de ejecutar.
2. No abusar de bloques `try` gigantescos. Cuanto menos código haya dentro del `try`, menos probabilidad de silenciar bugs ajenos a la excepción que queremos controlar.
3. Durante el desarrollo, capturar `Exception as e` permite ver mensajes como `"name 'prin' is not defined"`, revelando el error tipográfico inmediatamente.

#### <mark style="color:$danger;">Mejora del código</mark>

Una mejor versión del ejemplo incluiría un manejo genérico de excepciones que permita identificar errores no previstos:

```python
try:
    valor = int(input("Ingrese un número: "))
    resultado = 10 / valor
    print(f"Resultado: {resultado}")
except ZeroDivisionError:
    print("Error: División por cero.")
except Exception as e:
    print(f"Error inesperado: {e}")
```

Ahora, cualquier excepción no contemplada explícitamente será capturada y reportada, ayudando al desarrollador a identificar y corregir errores de forma más eficiente.
