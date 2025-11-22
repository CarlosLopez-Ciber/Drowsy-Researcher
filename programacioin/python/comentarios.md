# Comentarios

En programación, un **comentario** es un fragmento de texto dentro del código fuente que el intérprete ignora deliberadamente durante la ejecución. Su propósito no es funcional, sino comunicativo: sirve para explicar la lógica compleja, dejar notas de desarrollo o advertencias para otros programadores (incluyendo al propio autor en el futuro).

### <mark style="color:yellow;">1. El Estándar: Símbolo Numeral (</mark><mark style="color:yellow;">`#`</mark><mark style="color:yellow;">)</mark>

La forma oficial y sintáctica de escribir un comentario en Python es mediante el símbolo `#`. El intérprete omitirá cualquier texto que se encuentre desde este símbolo hasta el final de la línea física.

Existen dos variantes de uso:

#### <mark style="color:$danger;">Comentarios de Bloque</mark>

Se colocan antes del código que describen y suelen usar líneas completas.

```python
# Calcula el área de un círculo
# Fórmula: pi * radio al cuadrado
radio = 5
area = 3.1416 * (radio ** 2)
```

#### <mark style="color:$danger;">Comentarios en Línea (Inline)</mark>

Se colocan en la misma línea de la instrucción, separados por al menos dos espacios del código.

```python
x = 10  # Inicializamos la variable x
```

***

### <mark style="color:yellow;">2. Bloques Multilínea: Comillas Triples</mark>

Python no tiene una sintaxis específica para "comentarios de bloque multilínea" (como el `/* ... */` de C o Java). Sin embargo, se utiliza una convención aceptada: el uso de comillas triples (`"""` o `'''`).

```python
"""
Este es un bloque de texto
que abarca varias líneas
y funciona visualmente como un comentario.
"""
usuario = "Admin"
```

#### <mark style="color:$danger;">Distinción Técnica: Cadenas vs. Comentarios</mark>

Es crucial entender la diferencia técnica: **Las comillas triples crean una cadena de texto (`str`), no un comentario.**

Si escribes esto en la consola interactiva, verás que Python evalúa el texto y lo devuelve como un objeto:

```python
>>> """
... Comentario
... de prueba
... """
'\nComentario\nde prueba\n'
```

¿Por qué se usa como comentario entonces?

Funciona porque es una Cadena Literal No Asignada (Unassigned String Literal).

Al escribir una cadena sin asignarla a una variable (ej. texto = "..."), se convierte en una "sentencia de expresión". El intérprete evalúa la cadena, crea el objeto en memoria, pero al ver que no se guarda en ninguna referencia, el Recolector de Basura (Garbage Collector) eventualmente la descarta o simplemente se ignora en el bytecode final optimizado.

Por lo tanto, aunque técnicamente es código ejecutable (una creación de string), en la práctica actúa como un comentario inerte.

***

### <mark style="color:yellow;">3. Docstrings: El Uso Real de las Comillas Triples</mark>

Aunque usar comillas triples como comentarios "sueltos" es válido, su propósito real en Python es la **Documentación** (Docstrings).

Si colocas una cadena de comillas triples **en la primera línea** de una función, clase o módulo, Python no la descarta. La guarda en un atributo especial llamado `__doc__`.

```python
def saludar():
    """
    Esta función imprime un saludo.
    Es la documentación oficial de la función.
    """
    print("Hola")
```

Esta es la información que aparece cuando ejecutas `help(saludar)`.
