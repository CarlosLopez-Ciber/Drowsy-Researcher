# Texto en Python - Cadenas (Strings)

Las cadenas de texto (o `str`) son, sin duda, uno de los tipos de datos que más usarás. En Python, una cadena es la forma en que representamos cualquier tipo de texto.

> **Definición Clave:** Una cadena es una **secuencia inmutable de caracteres Unicode**.

Suena técnico, pero es simple si lo dividimos en sus tres partes.

***

### <mark style="color:orange;">¿Qué Significa "Secuencia Inmutable de Caracteres Unicode"?</mark>

#### <mark style="color:green;">1. Secuencia (Ordenada)</mark>

Significa que es una **serie ordenada** de elementos. En este caso, los elementos son **caracteres** (letras, números, símbolos). Al igual que una lista, cada carácter tiene un índice (posición) fijo.

```
texto = "Hola"
# H -> índice 0
# o -> índice 1
# l -> índice 2
# a -> índice 3
```

#### <mark style="color:green;">2. Inmutable (No se puede cambiar)</mark>

Esto es muy importante: **no puedes cambiar un carácter individual** dentro de una cadena una vez creada. Si intentas hacerlo, obtendrás un error.

```
mensaje = "Hola"
# Esto generará un error:
# mensaje[0] = "C"  # TypeError!
```

Si necesitas "modificar" una cadena, lo que realmente haces es crear una _nueva cadena_ y reasignar la variable.

```
mensaje = "Hola"
mensaje = "Chao"  # Esto es válido, 'mensaje' ahora apunta a una cadena nueva
print(mensaje)
# Output: Chao
```

#### <mark style="color:green;">3. Caracteres Unicode</mark>

Python usa el estándar **Unicode** por defecto. Esto es una ventaja enorme, ya que nos permite representar símbolos de casi todos los idiomas del mundo, emojis, acentos y caracteres especiales sin ningún problema.

```
emoji = "😊"
texto_acentuado = "¡Buenos días!"
chino = "你好"
árabe = "مرحبا"

print(f"{emoji} {texto_acentuado} {chino} {árabe}")
# Output: 😊 ¡Buenos días! 你好 مرحبا
```

Todo eso es texto válido en Python.

***

### <mark style="color:orange;">Creando Cadenas: Las Comillas</mark>

Puedes definir cadenas usando comillas **simples (`'`)** o **dobles (`"`)**. Ambas son idénticas en funcionalidad.

```
cadena1 = "Esto es una cadena de texto."
cadena2 = 'Esto también es una cadena de texto.'
```

> Python te da esta flexibilidad para que sea fácil incluir un tipo de comilla dentro del otro sin tener que "escapar" caracteres.

```
# Usamos comillas simples para contener las dobles
mensaje1 = 'Le dije a mi amigo, "¡Python es mi lenguaje favorito!"'

# Usamos comillas dobles para contener el apóstrofe (comilla simple)
mensaje2 = "El lenguaje 'Python' lleva el nombre de Monty Python."
```

#### <mark style="color:green;">Cadenas Multilínea</mark>

Para definir cadenas que ocupan varias líneas, se usan **comillas triples** (`'''` o `"""`). Esto es muy útil para párrafos largos o para guardar _scripts_ de otros lenguajes (como SQL) dentro de Python.

```
texto = """Python es un lenguaje versátil.
Puedes usarlo para desarrollo web, automatización, 
ciencia de datos, y más."""

print(texto)
```

**Salida:**

```
Python es un lenguaje versátil.
Puedes usarlo para desarrollo web, automatización, 
ciencia de datos, y más.
```

***

### <mark style="color:green;">f-strings (Formateo)</mark>

Las **f-strings** (_formatted string literals_) son la forma moderna (desde Python 3.6), rápida y legible de **incrustar variables y expresiones dentro de cadenas**.

> Se definen poniendo una `f` justo antes de la comilla de apertura. Luego, pones tus variables o código Python entre llaves `{}`.

#### Ejemplo

```
nombre = "ada"
apellido = "lovelace"
nombre_completo = f"{nombre} {apellido}"
print(nombre_completo)
```

**Salida:**

```
ada lovelace
```

Como puedes ver, Python reemplaza `{nombre}` y `{apellido}` por sus valores.

#### <mark style="color:green;">Uso en Mensajes Dinámicos</mark>

Las f-strings te permiten ejecutar código dentro de las llaves, como llamar a un método:

```
primer_nombre = "ada"
apellido = "lovelace"
nombre_completo = f"{primer_nombre} {apellido}"

print(f"Hola, {nombre_completo.title()}!")
```

**Salida:**

```
Hola, Ada Lovelace!
```

#### <mark style="color:green;">Asignación de Mensajes a Variables</mark>

Es una buena práctica guardar tu f-string en una variable si la vas a usar varias veces.

```
usuario = "lucia"
edad = 28
pais = "Perú"

perfil = f"Usuario: {usuario.title()} | Edad: {edad} | País: {pais.upper()}"
print(perfil)
```

**Salida:**

```
Usuario: Lucia | Edad: 28 | País: PERÚ
```

***

### <mark style="color:orange;">Controlando el Formato: Caracteres de Escape</mark>

Puedes incluir caracteres especiales que no son "visibles" para controlar el formato. Los más comunes se "escapan" con una barra invertida `\`.

* `\t` → Inserta una **Tabulación** (una sangría).
* `\n` → Inserta una **Nueva Línea** (un salto de línea).

#### <mark style="color:green;">Tabulaciones con</mark> <mark style="color:green;"></mark><mark style="color:green;">`\t`</mark>

```
print("Python")
print("\tPython") # Con sangría
```

**Salida:**

```
Python
	Python
```

#### <mark style="color:green;">Nuevas Líneas con</mark> <mark style="color:green;"></mark><mark style="color:green;">`\n`</mark>

```
print("Lenguajes:\nPython\nC\nJavaScript")
```

**Salida:**

```
Lenguajes:
Python
C
JavaScript
```

#### <mark style="color:green;">Combinación de</mark> <mark style="color:green;"></mark><mark style="color:green;">`\n`</mark> <mark style="color:green;"></mark><mark style="color:green;">y</mark> <mark style="color:green;"></mark><mark style="color:green;">`\t`</mark>

Puedes usarlos juntos para crear listas limpias y estructuradas, muy útil para reportes o menús.

```
print("Lenguajes:\n\t- Python\n\t- C\n\t- JavaScript")
```

**Salida:**

```
Lenguajes:
	- Python
	- C
	- JavaScript
```

***

### <mark style="color:orange;">Guía de Referencia: Los Métodos de String</mark>

Para el día a día, usarás `strip()`, `lower()`, `upper()`, `title()`, `split()`, `join()` y `replace()`. Pero a veces, necesitas algo más específico.

| **Método**                                             | **Descripción en Español**                                                                                                                                                                                                                                                                                                                                                                                                         |
| ------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **capitalize(self, /)**                                | Devuelve una versión "capitalizada" de la cadena. Más específicamente, convierte el primer carácter a mayúscula y el resto a minúsculas.                                                                                                                                                                                                                                                                                           |
| **casefold(self, /)**                                  | Devuelve una versión de la cadena adecuada para comparaciones sin distinción de mayúsculas/minúsculas (caseless).                                                                                                                                                                                                                                                                                                                  |
| **center(self, width, fillchar=' ', /)**               | Devuelve una cadena centrada de longitud `width`. El relleno se realiza usando el carácter de relleno (`fillchar`) especificado (por defecto es un espacio).                                                                                                                                                                                                                                                                       |
| **count(...)**                                         | `S.count(sub[, start[, end]]) -> int` Devuelve el número de apariciones que no se solapan de la subcadena `sub` en la cadena `S[start:end]`. Los argumentos opcionales `start` y `end` se interpretan como en la notación de rebanado (slicing).                                                                                                                                                                                   |
| **encode(self, /, encoding='utf-8', errors='strict')** | Codifica la cadena usando el códec registrado para la codificación (`encoding`). `encoding` La codificación en la que se codificará la cadena. `errors` El esquema de manejo de errores a usar. El valor por defecto es `'strict'`, lo que significa que los errores de codificación lanzan un `UnicodeEncodeError`. Otros valores posibles son `'ignore'`, `'replace'`, `'xmlcharrefreplace'` y cualquier otro nombre registrado. |
| **endswith(...)**                                      | `S.endswith(suffix[, start[, end]]) -> bool` Devuelve `True` si S termina con el `suffix` (sufijo) especificado, `False` en caso contrario. Con `start` opcional, prueba S comenzando en esa posición. Con `end` opcional, deja de comparar S en esa posición. `suffix` también puede ser una tupla de cadenas a probar.                                                                                                           |
| **expandtabs(self, /, tabsize=8)**                     | Devuelve una copia donde todos los caracteres de tabulación (`\t`) se expanden usando espacios. Si no se proporciona `tabsize`, se asume un tamaño de tabulación de 8 caracteres.                                                                                                                                                                                                                                                  |
| **find(...)**                                          | `S.find(sub[, start[, end]]) -> int` Devuelve el índice más bajo en S donde se encuentra la subcadena `sub`, tal que `sub` esté contenida en `S[start:end]`. Los argumentos opcionales `start` y `end` se interpretan como en la notación de rebanado. Devuelve `-1` si no se encuentra.                                                                                                                                           |
| **format(...)**                                        | `S.format(*args, **kwargs) -> str` Devuelve una versión formateada de S, usando sustituciones de `args` y `kwargs`. Las sustituciones se identifican mediante llaves (`{` y `}`).                                                                                                                                                                                                                                                  |
| **format\_map(...)**                                   | `S.format_map(mapping) -> str` Devuelve una versión formateada de S, usando sustituciones de un `mapping` (mapeo). Las sustituciones se identifican mediante llaves (`{` y `}`).                                                                                                                                                                                                                                                   |
| **index(...)**                                         | `S.index(sub[, start[, end]]) -> int` Devuelve el índice más bajo en S donde se encuentra la subcadena `sub`, tal que `sub` esté contenida en `S[start:end]`. Los argumentos opcionales `start` y `end` se interpretan como en la notación de rebanado. Lanza `ValueError` si no se encuentra la subcadena.                                                                                                                        |
| **isalnum(self, /)**                                   | Devuelve `True` si la cadena es alfanumérica, `False` en caso contrario. Una cadena es alfanumérica si todos sus caracteres son alfanuméricos y hay al menos un carácter.                                                                                                                                                                                                                                                          |
| **isalpha(self, /)**                                   | Devuelve `True` si la cadena es alfabética, `False` en caso contrario. Una cadena es alfabética si todos sus caracteres son alfabéticos y hay al menos un carácter.                                                                                                                                                                                                                                                                |
| **isascii(self, /)**                                   | Devuelve `True` si todos los caracteres de la cadena son ASCII, `False` en caso contrario. Los caracteres ASCII tienen puntos de código en el rango U+0000-U+007F. La cadena vacía también es ASCII.                                                                                                                                                                                                                               |
| **isdecimal(self, /)**                                 | Devuelve `True` si la cadena es una cadena decimal, `False` en caso contrario. Una cadena es decimal si todos sus caracteres son decimales y hay al menos un carácter.                                                                                                                                                                                                                                                             |
| **isdigit(self, /)**                                   | Devuelve `True` si la cadena es una cadena de dígitos, `False` en caso contrario. Una cadena es de dígitos si todos sus caracteres son dígitos y hay al menos un carácter.                                                                                                                                                                                                                                                         |
| **isidentifier(self, /)**                              | Devuelve `True` si la cadena es un identificador válido de Python, `False` en caso contrario. Llama a `keyword.iskeyword(s)` para probar si la cadena `s` es un identificador reservado, como "def" o "class".                                                                                                                                                                                                                     |
| **islower(self, /)**                                   | Devuelve `True` si la cadena está en minúsculas, `False` en caso contrario. Una cadena está en minúsculas si todos los caracteres "con caja" (cased) están en minúscula y hay al menos un carácter "con caja".                                                                                                                                                                                                                     |
| **isnumeric(self, /)**                                 | Devuelve `True` si la cadena es numérica, `False` en caso contrario. Una cadena es numérica si todos sus caracteres son numéricos y hay al menos un carácter.                                                                                                                                                                                                                                                                      |
| **isprintable(self, /)**                               | Devuelve `True` si la cadena es imprimible, `False` en caso contrario. Una cadena es imprimible si todos sus caracteres se consideran imprimibles en `repr()` o si está vacía.                                                                                                                                                                                                                                                     |
| **isspace(self, /)**                                   | Devuelve `True` si la cadena es de espacios en blanco, `False` en caso contrario. Una cadena es de espacios en blanco si todos sus caracteres son espacios en blanco y hay al menos un carácter.                                                                                                                                                                                                                                   |
| **istitle(self, /)**                                   | Devuelve `True` si la cadena tiene formato de título ("title-cased"), `False` en caso contrario. En una cadena con formato de título, los caracteres en mayúscula o "title-case" solo pueden seguir a caracteres sin "caja" (uncased), y los caracteres en minúscula solo a caracteres "con caja" (cased).                                                                                                                         |
| **isupper(self, /)**                                   | Devuelve `True` si la cadena está en mayúsculas, `False` en caso contrario. Una cadena está en mayúsculas si todos los caracteres "con caja" (cased) están en mayúscula y hay al menos un carácter "con caja".                                                                                                                                                                                                                     |
| **join(self, iterable, /)**                            | Concatena cualquier número de cadenas. La cadena cuyo método se llama se inserta entre cada cadena del `iterable`. El resultado se devuelve como una nueva cadena. Ejemplo: `'.'.join(['ab', 'pq', 'rs']) -> 'ab.pq.rs'`                                                                                                                                                                                                           |
| **ljust(self, width, fillchar=' ', /)**                | Devuelve una cadena justificada a la izquierda de longitud `width`. El relleno se realiza usando el carácter de relleno especificado (por defecto es un espacio).                                                                                                                                                                                                                                                                  |
| **lower(self, /)**                                     | Devuelve una copia de la cadena convertida a minúsculas.                                                                                                                                                                                                                                                                                                                                                                           |
| **lstrip(self, chars=None, /)**                        | Devuelve una copia de la cadena con los espacios en blanco iniciales (leading) eliminados. Si se proporciona `chars` y no es `None`, elimina los caracteres que estén en `chars` en su lugar.                                                                                                                                                                                                                                      |
| **partition(self, sep, /)**                            | Divide la cadena en tres partes usando el separador (`sep`) dado. Busca el separador; si se encuentra, devuelve una 3-tupla con: (la parte antes del separador, el separador mismo, la parte después del separador). Si no se encuentra el separador, devuelve una 3-tupla con: (la cadena original, una cadena vacía, una cadena vacía).                                                                                          |
| **removeprefix(self, prefix, /)**                      | Devuelve una cadena con el prefijo (`prefix`) dado eliminado, si está presente. Si la cadena comienza con el prefijo, devuelve `cadena[len(prefix):]`. En caso contrario, devuelve una copia de la cadena original.                                                                                                                                                                                                                |
| **removesuffix(self, suffix, /)**                      | Devuelve una cadena con el sufijo (`suffix`) dado eliminado, si está presente. Si la cadena termina con el sufijo y este no está vacío, devuelve `cadena[:-len(suffix)]`. En caso contrario, devuelve una copia de la cadena original.                                                                                                                                                                                             |
| **replace(self, old, new, count=-1, /)**               | Devuelve una copia con todas las apariciones de la subcadena `old` reemplazadas por `new`. `count` Número máximo de apariciones a reemplazar. -1 (el valor por defecto) significa reemplazar todas las apariciones. Si se proporciona `count`, solo se reemplazan las primeras `count` apariciones.                                                                                                                                |
| **rfind(...)**                                         | `S.rfind(sub[, start[, end]]) -> int` Devuelve el índice más alto en S donde se encuentra la subcadena `sub`, tal que `sub` esté contenida en `S[start:end]`. Argumentos opcionales se interpretan como en la notación de rebanado. Devuelve `-1` si no se encuentra.                                                                                                                                                              |
| **rindex(...)**                                        | `S.rindex(sub[, start[, end]]) -> int` Devuelve el índice más alto en S donde se encuentra la subcadena `sub`, tal que `sub` esté contenida en `S[start:end]`. Argumentos opcionales se interpretan como en la notación de rebanado. Lanza `ValueError` si no se encuentra la subcadena.                                                                                                                                           |
| **rjust(self, width, fillchar=' ', /)**                | Devuelve una cadena justificada a la derecha de longitud `width`. El relleno se realiza usando el carácter de relleno especificado (por defecto es un espacio).                                                                                                                                                                                                                                                                    |
| **rpartition(self, sep, /)**                           | Divide la cadena en tres partes usando el separador (`sep`) dado. Busca el separador comenzando desde el final; si se encuentra, devuelve una 3-tupla con: (la parte antes del separador, el separador mismo, la parte después del separador). Si no se encuentra el separador, devuelve una 3-tupla con: (una cadena vacía, una cadena vacía, la cadena original).                                                                |
| **rsplit(self, /, sep=None, maxsplit=-1)**             | Devuelve una lista de las subcadenas de la cadena, usando `sep` como separador. `sep` El separador usado para dividir. Si es `None` (por defecto), divide por cualquier espacio en blanco y descarta cadenas vacías. `maxsplit` Número máximo de divisiones. -1 (por defecto) significa sin límite. La división comienza al final de la cadena y avanza hacia el principio.                                                        |
| **rstrip(self, chars=None, /)**                        | Devuelve una copia de la cadena con los espacios en blanco finales (trailing) eliminados. Si se proporciona `chars` y no es `None`, elimina los caracteres que estén en `chars` en su lugar.                                                                                                                                                                                                                                       |
| **split(self, /, sep=None, maxsplit=-1)**              | Devuelve una lista de las subcadenas de la cadena, usando `sep` como separador. `sep` El separador usado para dividir. Si es `None` (por defecto), divide por cualquier espacio en blanco y descarta cadenas vacías. `maxsplit` Número máximo de divisiones (comenzando desde la izquierda). -1 (por defecto) significa sin límite.                                                                                                |
| **splitlines(self, /, keepends=False)**                | Devuelve una lista de las líneas de la cadena, dividiendo en los límites de línea (saltos de línea). Los saltos de línea no se incluyen en la lista resultante, a menos que `keepends` se proporcione y sea `True`.                                                                                                                                                                                                                |
| **startswith(...)**                                    | `S.startswith(prefix[, start[, end]]) -> bool` Devuelve `True` si S comienza con el `prefix` (prefijo) especificado, `False` en caso contrario. Con `start` opcional, prueba S comenzando en esa posición. Con `end` opcional, deja de comparar S en esa posición. `prefix` también puede ser una tupla de cadenas a probar.                                                                                                       |
| **strip(self, chars=None, /)**                         | Devuelve una copia de la cadena con los espacios en blanco iniciales (leading) y finales (trailing) eliminados. Si se proporciona `chars` y no es `None`, elimina los caracteres que estén en `chars` en su lugar.                                                                                                                                                                                                                 |
| **swapcase(self, /)**                                  | Convierte caracteres en mayúscula a minúscula y caracteres en minúscula a mayúscula.                                                                                                                                                                                                                                                                                                                                               |
| **title(self, /)**                                     | Devuelve una versión de la cadena donde cada palabra tiene formato de título ("titlecased"). Más específicamente, las palabras comienzan con caracteres en mayúscula y todos los caracteres "con caja" restantes están en minúscula.                                                                                                                                                                                               |
| **translate(self, table, /)**                          | Reemplaza cada carácter de la cadena usando la tabla de traducción (`table`) dada. `table` Tabla de traducción, que debe ser un mapeo de ordinales Unicode a ordinales Unicode, cadenas, o `None`. Debe implementar la búsqueda (ej. un diccionario o lista). Si la operación falla, el carácter se deja intacto. Los caracteres mapeados a `None` se eliminan.                                                                    |
| **upper(self, /)**                                     | Devuelve una copia de la cadena convertida a mayúsculas.                                                                                                                                                                                                                                                                                                                                                                           |
| **zfill(self, width, /)**                              | Rellena una cadena numérica con ceros (`0`) a la izquierda, para llenar un campo del `width` (ancho) dado. La cadena nunca se trunca.                                                                                                                                                                                                                                                                                              |

***

### <mark style="color:orange;">¿Dudas? ¡Usa</mark> <mark style="color:orange;"></mark><mark style="color:orange;">`help(str)`</mark><mark style="color:orange;">!</mark>

Si alguna vez olvidas un método o cómo funciona, puedes usar la función `help()` directamente en tu terminal de Python para ver la documentación oficial.

```
# Ejecuta esto en una terminal de Python
help(str)
```

> <mark style="color:yellow;">Si no logras comprender la información mostrada por la documentación (es muy técnica), copia la información y pídele a tu IA de confianza una mayor explicación.</mark>
