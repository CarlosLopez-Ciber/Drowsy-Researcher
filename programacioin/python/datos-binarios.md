# Datos Binarios

### <mark style="color:yellow;">La Dualidad de los Datos en Python</mark>

En Python, la información se gestiona en dos dominios distintos:

1. **Dominio del Texto (`str`):** Abstracción de alto nivel diseñada para humanos. Contiene caracteres Unicode (letras, símbolos, ideogramas).
2. **Dominio de la Máquina (`bytes`):** Representación de bajo nivel. Contiene la secuencia cruda de números (0-255) que la computadora procesa realmente.

Todo archivo en disco, paquete de red o imagen es, en su nivel fundamental, una secuencia de bytes. Python _decodifica_ estos bytes a `str` para facilitar su lectura, pero a veces es necesario manipular los datos crudos directamente.

***

### <mark style="color:yellow;">1.</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">`bytes`</mark><mark style="color:yellow;">: Secuencias Binarias Inmutables</mark>

> **Definición:** Un objeto `bytes` es una secuencia **inmutable** de enteros en el rango 0-255.

#### <mark style="color:$danger;">Sintaxis y Representación</mark>

Se definen anteponiendo el prefijo `b` a las comillas.

```python
# Definición hexadecimal explícita (bytes 2 y 31)
datos_crudos = b'\x02\x1f'

print(datos_crudos)       # Salida: b'\x02\x1f'
print(type(datos_crudos)) # Salida: <class 'bytes'>
```

#### <mark style="color:$danger;">La Ilusión ASCII</mark>

Python intenta ser amigable al mostrar objetos `bytes`. Si un byte corresponde a un carácter ASCII imprimible (como letras o números), lo mostrará como tal. Si no, mostrará su código hexadecimal (`\xNN`).

```python
# El byte 65 es 'A' en ASCII
mix_bytes = b'\x41\x02\x1f'

print(mix_bytes)
# Salida: b'A\x02\x1f'
```

**Importante:** Aunque veas una 'A', internamente es el número 65.

#### <mark style="color:$danger;">Comportamiento de Indexación</mark>

Esta es la prueba definitiva para distinguir `str` de `bytes`.

* Indexar un `str` devuelve un carácter (`str`).
* Indexar un `bytes` devuelve un número entero (`int`).

```python
texto = "ABC"
binario = b"ABC"

print(type(texto[0]))   # <class 'str'> (Es la letra "A")
print(type(binario[0])) # <class 'int'> (Es el número 65)
```

***

### <mark style="color:yellow;">2.</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">`bytearray`</mark><mark style="color:yellow;">: Secuencias Binarias Mutables</mark>

Si `bytes` es la versión inmutable (similar a una tupla), `bytearray` es la versión **mutable** (similar a una lista). Permite modificar los bytes individuales in situ, lo cual es eficiente para buffers de datos o construcción de paquetes de red.

#### <mark style="color:$danger;">Creación y Modificación</mark>

```python
# Constructor desde un literal de bytes
buffer = bytearray(b'\x41\x42\x43') # Bytes 65, 66, 67 ('ABC')

print(buffer)
# Salida: bytearray(b'ABC')
```

Para modificar un `bytearray`, debemos asignar **enteros** (0-255) a sus índices.

```python
# Modificar un solo byte
# Cambiamos el índice 0 (65/'A') por 99 (que es 'c')
buffer[0] = 99 

print(buffer)
# Salida: bytearray(b'cBC')
```

También admite asignación por rebanado (slice), pero en este caso se deben asignar objetos tipo bytes.

```python
# Reemplazar un rango
buffer[1:3] = b'\x01\x02'
print(buffer)
# Salida: bytearray(b'c\x01\x02')
```

***

### <mark style="color:yellow;">3. El Puente: Codificación y Decodificación</mark>

El paso entre `str` y `bytes` no es automático; requiere una conversión explícita basada en una tabla de codificación (como UTF-8 o ASCII).

* **`encode()`**: De Humano (`str`) a Máquina (`bytes`).
* **`decode()`**: De Máquina (`bytes`) a Humano (`str`).

```python
mensaje = "Hola 🐍" # Incluye emoji (multibyte)

# 1. Codificar (String -> Bytes)
datos_binarios = mensaje.encode('utf-8')
print(datos_binarios)
# Salida: b'Hola \xf0\x9f\x90\x8d'
# Nota: El emoji se convirtió en 4 bytes (\xf0\x9f\x90\x8d)

# 2. Decodificar (Bytes -> String)
mensaje_recuperado = datos_binarios.decode('utf-8')
print(mensaje_recuperado)
# Salida: Hola 🐍
```

***

### <mark style="color:yellow;">4. Operaciones Avanzadas</mark>

#### <mark style="color:$danger;">Aritmética de Secuencias</mark>

Al igual que listas y tuplas, los tipos binarios soportan concatenación y repetición.

```python
header = b'\x01\x02'
payload = b'\xFF'

paquete = header + payload
print(paquete) # b'\x01\x02\xff'
```

#### <mark style="color:$danger;">Conversión Binario-Entero (</mark><mark style="color:$danger;">`int.from_bytes`</mark><mark style="color:$danger;">)</mark>

En protocolos de red o lectura de sensores, es común recibir un número fragmentado en varios bytes (ej. un entero de 16 bits dividido en dos bytes).

```python
# Bytes que representan el número 543
# \x02 = 2
# \x1f = 31
# Cálculo Big Endian: (2 * 256) + 31 = 543
bytes_numero = b'\x02\x1f'

numero = int.from_bytes(bytes_numero, byteorder='big')
print(numero)
# Salida: 543
```
