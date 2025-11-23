# Alias y Buenas Prácticas de Importación

### <mark style="color:yellow;">La Palabra Clave</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">`as`</mark><mark style="color:yellow;">: Creación de Alias</mark>

Python permite renombrar un módulo o una entidad en el momento exacto de su importación mediante la palabra clave `as`. Esto crea un **alias** (seudónimo) bajo el cual el objeto será accesible en el script actual.

#### <mark style="color:$danger;">A. Alias de Módulo (Renombrado Completo)</mark>

Es extremadamente útil para librerías con nombres largos o jerarquías complejas.

**Caso de Uso: Concisión**

En ciencia de datos, es un estándar industrial usar alias cortos para librerías populares.

```python
# En lugar de escribir matplotlib.pyplot.plot(...)
import matplotlib.pyplot as plt

plt.plot([1, 2, 3]) 
```

**Caso de Uso: Resolución de Conflictos**

Si tu script ya utiliza un nombre de variable que coincide con un módulo que necesitas importar, puedes usar un alias para evitar la colisión.

```python
# Ya tenemos una variable llamada 'math'
math = "Matemáticas Básicas"

# Importamos el módulo con otro nombre para no romper nuestra variable
import math as _math_utils 

print(math)              # "Matemáticas Básicas"
print(_math_utils.sqrt(4)) # 2.0
```

#### <mark style="color:$danger;">B. Alias de Entidad (Renombrado Selectivo)</mark>

También puedes aplicar alias a funciones o variables específicas importadas mediante `from`.

```python
from math import pi as constante_universal_pi

print(constante_universal_pi) 
# Salida: 3.141592...
```

Esto es útil para dar contexto semántico a una función genérica o para desambiguar dos funciones con el mismo nombre de módulos distintos.

**Restricción Técnica:**

`as` es una palabra reservada del lenguaje. No puedes usarla como nombre de variable (ej. as = 5 generará un SyntaxError).
