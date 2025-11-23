# Metodología de Investigación y Descubrimiento de Herramientas

Un error común al aprender Python es intentar memorizar cada función o método disponible. Python es inmenso y está en constante evolución; memorizarlo todo es imposible e ineficiente.

La habilidad más valiosa de un programador no es saber la respuesta, sino **saber dónde encontrarla**. Python es un lenguaje "introspectivo", lo que significa que el propio código puede decirte qué es y qué sabe hacer.

Referencia oficial constante: [Índice General de Python (Docs)](https://docs.python.org/es/3/genindex.html)

### <mark style="color:yellow;">1. Identificación de Clases:</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">`type()`</mark>

Para manipular un objeto, primero es necesario conocer su naturaleza. La función `type()` devuelve la **clase** a la que pertenece el objeto. Este es el primer paso para buscar documentación externa.

```python
mi_lista = [1, 2, 3]
print(type(mi_lista))
# Salida: <class 'list'>
# Conclusión: Debo buscar documentación sobre "python list methods"

archivo = open("test.txt", "w")
print(type(archivo))
# Salida: <class '_io.TextIOWrapper'>
# Conclusión: Debo buscar documentación sobre "TextIOWrapper"
```

### <mark style="color:yellow;">2. Descubrimiento de Atributos:</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">`dir()`</mark>

Una vez conocida la clase, la función `dir()` (directorio) lista todos los atributos y métodos disponibles para ese objeto. Es útil para descubrir capacidades sin salir del código.

```python
mi_lista = [1, 2, 3]
print(dir(mi_lista))
```

**Salida (simplificada):**

```
['__add__', '__class__', ..., 'append', 'clear', 'copy', 'count', 'extend', 'index', 'insert', 'pop', 'remove', 'reverse', 'sort']
```

* **Métodos "Dunder" (`__x__`):** Los que comienzan y terminan con doble guion bajo son internos de Python (ej. `__add__` define cómo funciona el operador `+`). Generalmente se ignoran en el uso básico.
* **Métodos Públicos:** Los nombres limpios (ej. `append`, `pop`) son las herramientas que puedes utilizar directamente.

### <mark style="color:yellow;">3. Documentación en Línea:</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">`help()`</mark>

Habiendo identificado un método de interés con `dir()`, el siguiente paso es entender su sintaxis y argumentos. La función `help()` muestra la documentación integrada (docstring).

Es posible invocarla sobre el objeto, la clase o un método específico.

```python
mi_lista = [1, 2, 3]

# Consulta específica sobre el método 'append'
help(mi_lista.append)
```

**Salida:**

```
Help on built-in function append:

append(object, /)
    Append object to the end of the list.
```

### <mark style="color:yellow;">4. Interpretación de Errores (Traceback)</mark>

El _Traceback_ es el reporte que Python genera cuando ocurre una excepción. Lejos de ser solo una advertencia, contiene la información exacta para solucionar el problema.

**Regla de Oro:** Leer siempre la **última línea** primero.

#### Anatomía de un error

```python
>>> mi_lista = [1, 2, 3]
>>> mi_lista.append()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: append() takes exactly one argument (0 given)
```

1. **Ubicación:** `File "<stdin>", line 1` indica dónde ocurrió el fallo.
2. **Tipo de Error:** `TypeError` indica que la operación es inválida para ese tipo de dato.
3. **Descripción:** `append() takes exactly one argument (0 given)` explica la causa lógica: la función esperaba un dato entre paréntesis y no recibió ninguno.

### <mark style="color:yellow;">5. El Laboratorio: La Consola Interactiva (REPL)</mark>

La forma más eficiente de aplicar este flujo no es en el archivo final del proyecto, sino en la consola interactiva (REPL). Es un entorno aislado donde los errores no tienen consecuencias.

Para acceder, ejecuta `python` o `python3` en tu terminal. El prompt cambiará a `>>>`.

Utiliza este espacio para experimentar con `type`, `dir` y `help` antes de escribir el código definitivo en tu editor.
