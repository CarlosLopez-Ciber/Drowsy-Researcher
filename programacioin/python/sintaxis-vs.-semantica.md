# Sintaxis vs. Semántica

Al aprender a programar, existen dos pilares fundamentales que sostienen cualquier lenguaje: la **sintaxis** y la **semántica**. Entender la distinción entre ambas es crítico para diagnosticar errores. Una analogía útil es comparar la programación con el aprendizaje de un idioma humano:

1. La **Sintaxis** corresponde a las reglas gramaticales y ortográficas.
2. La **Semántica** corresponde al significado y la lógica del mensaje.

### <mark style="color:yellow;">1. Sintaxis: La gramática del código</mark>

La sintaxis es el conjunto estricto de reglas que definen cómo debe estructurarse el código para ser considerado válido por el intérprete. Si estas reglas se violan, el programa no puede iniciarse.

**Analogía en lenguaje natural:**

* _Incorrecto:_ `perro el corre rápido` (Violación de reglas gramaticales).<br>
* _Correcto:_ `El perro corre rápido` (Estructura válida).<br>

En Python:

Python impone reglas específicas, como el uso de dos puntos (:) al final de una declaración de control y la indentación obligatoria para definir bloques.

```python
# SINTAXIS INCORRECTA
# Faltan los dos puntos y la indentación
if 5 > 2
print("Cinco es mayor")
```

Al intentar ejecutar el código anterior, el intérprete detendrá el proceso inmediatamente y arrojará una excepción de tipo `SyntaxError` o `IndentationError`. El código no llega a ejecutarse.

### <mark style="color:yellow;">2. Semántica: El significado y la lógica</mark>

La semántica se refiere a lo que el código _hace_ realmente cuando se ejecuta. Un programa puede ser sintácticamente perfecto (sin errores de escritura) pero semánticamente incorrecto (hace algo distinto a lo deseado).

**Analogía en lenguaje natural:**

* _Sintaxis correcta, semántica incorrecta:_ `El gato ladra`.
  * Gramaticalmente, la oración es perfecta. Lógicamente, es un error: los gatos no ladran.<br>

En Python:

Los errores semánticos son conocidos como "errores lógicos". El programa se ejecuta de principio a fin sin detenerse, pero el resultado es erróneo.

_Ejemplo: Cálculo incorrecto de un promedio._

```python
# ERROR SEMÁNTICO (Lógico)
num1 = 10
num2 = 20

# Intención: Calcular el promedio de dos números.
# Error: Se divide por 3 en lugar de 2.
promedio = (num1 + num2) / 3

print(f"El promedio es: {promedio}")
# Salida: 10.0 (Incorrecto, debería ser 15.0)
```

En este caso, Python no genera ninguna alerta porque la operación matemática es válida, aunque la lógica aplicada por el programador sea incorrecta.

#### Semántica dependiente del contexto

El significado de una instrucción puede cambiar según el tipo de datos involucrados. Esto se observa claramente en operadores polimórficos como el símbolo `+`.

```python
# Semántica de SUMA (contexto numérico)
print(10 + 5)
# Salida: 15

# Semántica de CONCATENACIÓN (contexto de texto)
print("10" + "5")
# Salida: "105"
```

La sintaxis (`valor + valor`) es idéntica en ambos casos, pero la semántica cambia radicalmente según si los datos son enteros (`int`) o cadenas de texto (`str`).

***

### <mark style="color:yellow;">Comparativa de Errores</mark>

Comprender esta diferencia determina cómo abordamos la corrección de fallos (debugging):

| **Tipo de Error**      | **Detección**                                                                                                   | **Comportamiento**                                                                         |
| ---------------------- | --------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------ |
| **Error de Sintaxis**  | **Automática**. El editor o el intérprete indican la línea exacta y el tipo de fallo antes o durante el inicio. | El programa se detiene (crash). No produce resultados.                                     |
| **Error de Semántica** | **Manual**. Requiere revisión humana y pruebas. Es el tipo de error más difícil de rastrear.                    | El programa "funciona" y termina su ejecución, pero los datos resultantes son incorrectos. |

<br>
