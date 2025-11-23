# Funciones - Salida de Datos y Resultados

### <mark style="color:yellow;">1. La Sentencia</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">`return`</mark><mark style="color:yellow;">: Entrega y Finalización</mark>

Una función en Python puede tener dos propósitos: generar un **efecto secundario** (como imprimir en consola o guardar un archivo) o **devolver un valor** para ser procesado posteriormente. Para esto último, utilizamos la palabra clave `return`.

#### <mark style="color:$danger;">Mecánica de Ejecución</mark>

La instrucción `return` tiene un efecto doble e inmediato:

1. **Exportación:** Envía el valor de la expresión a la línea donde fue invocada la función.
2. **Terminación:** Detiene **inmediatamente** la ejecución de la función, ignorando cualquier código posterior dentro de su bloque.

**Sintaxis:**

```python
def calcular_total(precio, impuesto=0.18):
    if precio < 0:
        return 0  # Terminación anticipada (Guard Clause)
    
    return precio * (1 + impuesto) # Retorno de cálculo

# Captura del resultado en una variable
total = calcular_total(100)
print(f"Total: {total}")
```

#### <mark style="color:$danger;">El Patrón "Guard Clause"</mark>

El objetivo de una **Cláusula de Guarda** (Guard Clause) es verificar las condiciones de error al principio de la función y retornar inmediatamente. Esto evita el temido "código flecha" (múltiples niveles de indentación anidados) y deja el "camino feliz" (la ejecución exitosa) en el nivel principal de indentación.

Imagina una función que procesa un descuento para una compra. Requiere tres condiciones:

1. El precio debe ser positivo.
2. El usuario debe estar logueado.
3. El usuario debe tener una membresía activa.

**1. El Enfoque Tradicional (Anidamiento / "Código Flecha")**

Sin cláusulas de guarda, el código tiende a crecer hacia la derecha, haciéndose difícil de leer.

```python
def procesar_descuento(precio, usuario):
    if precio > 0:
        if usuario is not None:
            if usuario.get("es_miembro"):
                # --- Lógica Principal (El "Camino Feliz") ---
                descuento = precio * 0.20
                return precio - descuento
            else:
                return precio # Sin descuento para no miembros
        else:
            return None # Error: Usuario no existe
    else:
        return 0 # Error: Precio inválido
```

**Problemas de este enfoque:**

* La lógica principal está enterrada bajo 3 niveles de indentación.
* Es difícil rastrear qué `else` corresponde a qué `if`.
* Requiere mucha carga cognitiva para entender el flujo.

***

**2. El Enfoque con "Guard Clauses" (Recomendado)**

Aquí invertimos la lógica: verificamos los errores primero. Si encontramos un error, usamos `return` para salir inmediatamente. Si pasamos todas las guardas, ejecutamos la lógica principal sin indentación.

```python
def procesar_descuento(precio, usuario):
    # Guarda 1: Validación de datos básicos
    if precio <= 0:
        return 0
    
    # Guarda 2: Validación de existencia
    if usuario is None:
        return None
    
    # Guarda 3: Validación de reglas de negocio
    if not usuario.get("es_miembro"):
        return precio
    
    # --- Lógica Principal (El "Camino Feliz") ---
    # Nota cómo esto está en el primer nivel de indentación.
    # Solo llegamos aquí si TODO lo anterior fue válido.
    descuento = precio * 0.20
    return precio - descuento
```

**Ventajas Técnicas:**

1. **Linealidad:** El código se lee de arriba a abajo, no en zigzag.
2. **Validación Temprana:** La función falla rápido (Fail Fast). No pierde tiempo calculando nada si los datos de entrada son inválidos.
3. **Limpieza:** Elimina la necesidad de bloques `else` redundantes. Si el `if` ejecuta un `return`, el código que sigue es implícitamente el `else`.

***

### <mark style="color:yellow;">2. El Objeto</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">`None`</mark><mark style="color:yellow;">: La Ausencia de Valor</mark>

Si una función finaliza su ejecución sin encontrar una instrucción `return` explícita (o usa un `return` vacío), Python devuelve automáticamente un objeto especial: `None`.

#### Características Técnicas

* **Tipo:** Pertenece a la clase `NoneType`.
* **Operatividad:** No es un cero (`0`) ni una cadena vacía (`""`). Es un valor nulo. Intentar operar con él (ej. `None + 2`) genera un `TypeError`.
* **Singularidad:** Es un _singleton_; solo existe una instancia de `None` en el programa.

#### Comparación Segura

Para verificar si una función devolvió `None` (por ejemplo, en caso de error o búsqueda fallida), **nunca** uses el operador de igualdad `==`. La forma correcta y segura es usar el operador de identidad `is`.

```python
def buscar_usuario(id_usuario):
    if id_usuario == 0:
        return None  # Indica que no se encontró
    return {"id": id_usuario, "nombre": "Admin"}

usuario = buscar_usuario(0)

# Verificación Correcta
if usuario is None:
    print("Usuario no encontrado")
```

***

### <mark style="color:yellow;">3. Retorno de Estructuras Complejas (Listas)</mark>

Para dominar el paso de listas a funciones, debemos entender qué sucede realmente en la memoria RAM. Python no pasa los valores de la lista; pasa la **referencia** (la dirección de memoria) donde vive esa lista.

Esto crea dos escenarios posibles dentro de la función: **Mutación** (cambiar el contenido de la caja) vs. **Reasignación** (cambiar la etiqueta a otra caja).

**1. El Escenario de Mutación (Efecto Secundario)**

Cuando utilizas métodos que alteran la lista _in-situ_ (como `.append()`, `.extend()`, `.pop()`, `.sort()` o asignación por índice `lista[0] = x`), estás operando sobre **el mismo objeto físico** que se creó fuera de la función.

Como la variable externa (`mi_lista`) y la variable local (`lista`) apuntan al mismo objeto, los cambios son globales.

```python
def modificar_in_situ(referencia_lista):
    print(f"ID dentro (antes): {id(referencia_lista)}")
    
    # MUTACIÓN: Usamos un método del objeto. NO usamos el signo '='
    referencia_lista.append(999) 
    
    print(f"ID dentro (después): {id(referencia_lista)}")

numeros = [1, 2, 3]
print(f"ID original: {id(numeros)}")

modificar_in_situ(numeros)
print(f"Resultado final: {numeros}")
```

**Salida:**

```
ID original: 2483667968368
ID dentro (antes): 2483667968368
ID dentro (después): 2483667968368  <-- El ID nunca cambia
Resultado final: [1, 2, 3, 999]       <-- El cambio persiste
```

**2. El Escenario de Reasignación (Ruptura del Vínculo)**

Aquí es donde muchos se confunden. Si dentro de la función usas el operador de asignación (`=`) para darle un nuevo valor a la variable local, **rompes el vínculo** con el objeto original. Creas una nueva lista local y la variable externa queda intacta.

```python
def intentar_reasignar(referencia_lista):
    print(f"ID dentro (antes): {id(referencia_lista)}")
    
    # REASIGNACIÓN: El signo '=' crea un NUEVO objeto en memoria local
    referencia_lista = [999, 999, 999] 
    
    print(f"ID dentro (después): {id(referencia_lista)}") # ¡ID Nuevo!

numeros = [1, 2, 3]
intentar_reasignar(numeros)
print(f"Resultado final: {numeros}")
```

**Salida:**

```
ID dentro (antes): 2483667968368
ID dentro (después): 1928374655555  <-- ID diferente, es otro objeto
Resultado final: [1, 2, 3]            <-- La lista original NO cambió
```

**3. Estrategias de Protección de Datos (Copias)**

Si necesitas trabajar con los datos de una lista dentro de una función, pero **no** quieres que los cambios afecten a la lista original, debes pasar una **copia**, no la referencia original.

Existen dos formas estándar de hacerlo:

**A. Slicing Completo `[:]` (Clásico)**

Es rápido y muy común en código Python antiguo, aunque su sintaxis puede ser críptica para principiantes.

```python
def procesar(lista):
    lista.append("Procesado")
    return lista

original = [1, 2]
# Pasamos una copia. 'original' está seguro.
nueva = procesar(original[:]) 

print(original) # [1, 2]
print(nueva)    # [1, 2, 'Procesado']
```

**B. Método `.copy()` (Pythonic y Legible)**

Desde Python 3.3, las listas tienen un método explícito para esto. Es preferible por su claridad semántica.

```python
# Es obvio para cualquiera que lea el código que estamos copiando
nueva = procesar(original.copy())
```

Nota:

Ambos métodos (`[:]` y `.copy()`) crean una Copia Superficial (Shallow Copy). Si tu lista contiene otras listas dentro (ej. `[[1,2], [3,4]]`), la copia superficial protegerá la lista externa, pero las sub-listas internas seguirán compartiendo referencias. Para casos complejos anidados, se debe usar `import copy; copy.deepcopy()`. .

***

### <mark style="color:yellow;">4. Gestión del Valor de Retorno</mark>

Cuando una función ejecuta la instrucción `return`, coloca un valor en la pila de ejecución. Como programador, tienes total libertad para decidir el destino de ese valor. Existen tres patrones de diseño para manejar este retorno:

**1. Captura Explícita (Asignación)**

Este es el patrón más común. El valor devuelto por la función se almacena inmediatamente en una variable. Esto es necesario cuando el dato se requiere en múltiples lugares del código o en pasos posteriores del algoritmo.

Ejemplo:

Imagina una función que normaliza nombres de usuario. Necesitamos guardar el resultado para usarlo en la base de datos y en el email de bienvenida.

```python
def normalizar_usuario(nombre):
    return nombre.strip().lower()

# CAPTURA: Guardamos el resultado en la variable 'usuario_limpio'
raw_input = "  AdminUser  "
usuario_limpio = normalizar_usuario(raw_input)

# Usamos la variable capturada múltiples veces
print(f"Usuario registrado: {usuario_limpio}")
print(f"Email generado: {usuario_limpio}@empresa.com")
```

**2. Consumo Directo (Composición)**

No es obligatorio guardar el valor en una variable intermedia si solo se va a usar una vez. Puedes invocar la función directamente dentro de otra expresión (como un argumento de otra función, una operación matemática o una condición lógica). Python evalúa la función primero y usa su retorno en la expresión contenedora.

Ejemplo:

Validar si un número es par dentro de una condición if, sin crear una variable intermedia es\_par.

```python
def es_par(numero):
    return numero % 2 == 0

# CONSUMO DIRECTO: La llamada es parte de la expresión condicional
if es_par(10):
    print("El número 10 es par.")

# CONSUMO DIRECTO: La llamada es argumento de print()
print(f"¿El 5 es par? {es_par(5)}")
```

**3. Descarte Voluntario (Ignorar el Retorno)**

A veces, una función realiza una acción importante (Efecto Secundario) y además devuelve un dato (como un código de estado `True/False` o el objeto modificado). Si solo nos interesa la acción, podemos llamar a la función sin asignar su resultado a nada. El valor se devuelve, pero al no ser capturado, el Recolector de Basura de Python lo elimina eventualmente.

Ejemplo:

Una función que añade un elemento a una lista (efecto secundario) y devuelve el tamaño total de la lista (valor de retorno).

```python
def registrar_auditoria(lista_logs, mensaje):
    lista_logs.append(mensaje) # Efecto secundario: Modifica la lista
    return len(lista_logs)     # Retorno: Devuelve el nuevo tamaño

logs = []

# CASO A: Capturamos el valor porque nos interesa el tamaño
total = registrar_auditoria(logs, "Inicio de sesión")
print(f"Logs actuales: {total}")

# CASO B: Ignoramos el retorno (Descarte)
# Solo queremos guardar el log, no nos importa el tamaño actual.
# El valor '2' es devuelto, pero se pierde en el vacío.
registrar_auditoria(logs, "Cierre de sesión") 

print(logs) 
# Salida: ['Inicio de sesión', 'Cierre de sesión']
```

**Nota Técnica:** Ignorar el retorno es seguro y común en funciones como `list.sort()`, que ordena la lista in-situ y devuelve `None`, o `print()`, que escribe en pantalla y devuelve `None`. Sin embargo, ignorar el retorno de una función pura (una que no tiene efectos secundarios, como `suma(2,2)`) es inútil, ya que estarías gastando CPU para calcular un valor que nadie usará.
