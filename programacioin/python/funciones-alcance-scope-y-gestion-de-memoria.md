# Funciones - Alcance (Scope) y Gestión de Memoria

### <mark style="color:yellow;">1. Jerarquía de Alcances (Scope)</mark>

En Python, el "alcance" define la región del código donde una variable es visible y accesible. No todas las variables existen en todas partes. Python sigue la regla **LEGB** (Local, Enclosing, Global, Built-in), aunque aquí nos centraremos en los dos niveles principales.

#### <mark style="color:$danger;">A. Alcance Local (Función)</mark>

Cualquier variable definida **dentro** de una función es **local**.

* **Nacimiento:** Se crea cuando la función se ejecuta.
* **Muerte:** Se destruye automáticamente cuando la función termina (retorna).
* **Privacidad:** Es invisible para el código exterior.

```python
def mi_funcion():
    secreto = 12345  # Variable Local
    print(secreto)

mi_funcion()
print(secreto) 
# Error: NameError: name 'secreto' is not defined
```

#### <mark style="color:$danger;">B. Alcance Global (Módulo)</mark>

Cualquier variable definida en el cuerpo principal del script (fuera de cualquier función) es **global**.

* **Visibilidad:** Puede ser **leída** desde cualquier lugar, incluso dentro de las funciones.

```python
usuario = "Admin"  # Variable Global

def mostrar_usuario():
    # Lectura permitida
    print(f"Usuario actual: {usuario}") 

mostrar_usuario()
```

***

### <mark style="color:yellow;">2. El Fenómeno del Sombreado (Shadowing)</mark>

¿Qué pasa si una función intenta crear una variable con el mismo nombre que una global?

Python protege la variable global. Crea una **nueva variable local** con el mismo nombre que "tapa" (sombrea) a la global temporalmente dentro de la función.

```python
x = 10  # Global

def cambiar_x():
    x = 5  # Crea una NUEVA 'x' local. La global sigue siendo 10.
    print(f"X dentro: {x}")

cambiar_x()
print(f"X fuera: {x}")
```

**Salida:**

```
X dentro: 5
X fuera: 10
```

***

### <mark style="color:yellow;">3. Modificación Explícita: La palabra</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">`global`</mark>

Si realmente necesitas modificar una variable global desde dentro de una función (algo que generalmente se considera una mala práctica), debes pedir permiso explícito a Python usando la palabra clave `global`.

```python
contador = 0

def incrementar():
    global contador  # Aviso: "No crees una local, usa la de fuera"
    contador += 1

incrementar()
print(contador)  # Salida: 1
```

**Error común:** Si intentas hacer `contador += 1` sin declarar `global`, obtendrás un `UnboundLocalError` porque Python intenta sumar 1 a una variable local que aún no ha sido inicializada.

***

### <mark style="color:yellow;">4. Modelo de Paso de Argumentos en Memoria</mark>

Este es el concepto técnico más importante sobre funciones en Python. Python no usa "Paso por Valor" ni estrictamente "Paso por Referencia". Usa **"Paso por Asignación de Objeto"** (Call-by-Object-Reference).

Esto significa que la función recibe una referencia al objeto en memoria. El comportamiento depende de si ese objeto es **mutable** o **inmutable**.

#### <mark style="color:$danger;">Caso A: Objetos Inmutables (Enteros, Strings, Tuplas)</mark>

Se comportan como si fueran "copias". Modificar el parámetro dentro de la función **no afecta** a la variable original fuera de ella.

```python
def intentar_cambiar(numero):
    numero += 10
    print(f"Dentro: {numero}")

valor = 5
intentar_cambiar(valor)
print(f"Fuera: {valor}")  # Sigue siendo 5
```

**Razón:** Los enteros son inmutables. `numero += 10` crea un _nuevo_ objeto entero en memoria, dejando el original intacto.

#### <mark style="color:$danger;">Caso B: Objetos Mutables (Listas, Diccionarios)</mark>

Aquí es donde ocurren los efectos secundarios.

1.  **Mutación Directa (Peligro):** Si usas métodos que alteran el objeto (como `.append()` o `del`), el cambio **sí se refleja fuera**.

    ```python
    def agregar_item(lista):
        lista.append("Nuevo")  # Modifica el objeto compartido

    mi_lista = [1, 2]
    agregar_item(mi_lista)
    print(mi_lista)  # [1, 2, 'Nuevo'] -> ¡Cambió!
    ```
2.  **Reasignación (Seguro):** Si asignas una nueva lista al parámetro con `=`, rompes el vínculo con el objeto original.

    ```python
    def resetear_lista(lista):
        lista = []  # Apunta la variable local a una nueva lista vacía
        print(f"Dentro: {lista}")

    mi_lista = [1, 2]
    resetear_lista(mi_lista)
    print(f"Fuera: {mi_lista}")  # [1, 2] -> ¡Intacta!
    ```
