# Operadores de Pertenencia

En el manejo de datos, es una operación recurrente verificar si un elemento específico existe dentro de una colección mayor. Para realizar esta comprobación de manera eficiente y legible, Python proporciona los **operadores de pertenencia**.

Estos operadores evalúan la existencia de un objeto dentro de un "iterable" (contenedor) y devuelven un valor booleano.

| **Operador** | **Descripción**                                       | **Retorno**                |
| ------------ | ----------------------------------------------------- | -------------------------- |
| **`in`**     | Comprueba si el elemento **existe** en el contenedor. | `True` si se encuentra.    |
| **`not in`** | Comprueba la **ausencia** del elemento.               | `True` si NO se encuentra. |

***

### <mark style="color:yellow;">1. Uso en Cadenas de Texto (</mark><mark style="color:yellow;">`str`</mark><mark style="color:yellow;">)</mark>

Cuando se aplica a cadenas, el operador comprueba si una subcadena forma parte de la cadena principal.

**Sensibilidad:** La búsqueda es _case-sensitive_ (distingue mayúsculas de minúsculas).

```python
texto = "Python es potente"

# Búsqueda exitosa
print("potente" in texto)    # Salida: True

# Búsqueda fallida (por mayúscula)
print("python" in texto)     # Salida: False (La cadena contiene "Python")

# Búsqueda de ausencia
print("Java" not in texto)   # Salida: True
```

***

### <mark style="color:yellow;">2. Uso en Listas (</mark><mark style="color:yellow;">`list`</mark><mark style="color:yellow;">) y Tuplas</mark>

Este es el caso de uso más frecuente: validar si un elemento específico está almacenado en una secuencia.

```python
servidores = ["Apache", "Nginx", "IIS"]

# Verificación directa
print("Nginx" in servidores)
# Salida: True

# Verificación condicional (ejemplo lógico)
servidor_buscado = "Tomcat"
esta_presente = servidor_buscado in servidores

print(f"¿Está {servidor_buscado}?: {esta_presente}")
# Salida: ¿Está Tomcat?: False
```

***

### <mark style="color:yellow;">3. Uso en Diccionarios (</mark><mark style="color:yellow;">`dict`</mark><mark style="color:yellow;">)</mark>

El comportamiento en diccionarios tiene un matiz técnico importante que suele causar errores lógicos.

> **Regla Técnica:** Por defecto, la iteración sobre un diccionario se realiza únicamente sobre sus **CLAVES (keys)**, ignorando los valores.

```python
usuario = {
    "nombre": "Carlos",
    "rol": "Admin",
    "id": 505
}

# Búsqueda en CLAVES (Comportamiento por defecto)
print("nombre" in usuario)  # True (Existe la clave 'nombre')
print("Carlos" in usuario)  # False (NO busca en los valores)
```

#### <mark style="color:$danger;">Búsqueda en Valores</mark>

Para verificar si un valor existe dentro del diccionario, es necesario invocar explícitamente el método `.values()`.

```python
# Búsqueda explícita en VALORES
print("Carlos" in usuario.values()) # True
```

***

### <mark style="color:yellow;">Error Común: Iterabilidad en Tipos Atómicos</mark>

Los operadores de pertenencia requieren que el objeto de la derecha sea un **iterable** (una colección). Los tipos numéricos (`int`, `float`) son atómicos, no contienen elementos internos iterables.

Intentar usar `in` sobre un número generará una excepción `TypeError`.

```python
numero = 1345

# INTENTO ERRÓNEO
# print(1 in numero)
# Error: TypeError: argument of type 'int' is not iterable
```

Solución:

Si el objetivo es verificar si un dígito existe dentro de un número, se debe realizar una conversión de tipos (Casting) a cadena de texto (str).

```python
numero = 1345

# Conversión temporal a string para la búsqueda
print("1" in str(numero))
# Salida: True
```
