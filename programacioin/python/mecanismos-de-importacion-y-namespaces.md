# Mecanismos de Importación y Namespaces

### <mark style="color:yellow;">1. Concepto de Namespace (Espacio de Nombres)</mark>

Un **namespace** es un sistema lógico que Python utiliza para asociar nombres únicos a objetos (variables, funciones, clases). Técnicamente, es un mapeo (diccionario) que garantiza que un identificador sea único dentro de su contexto, aunque pueda repetirse en contextos diferentes.

#### <mark style="color:$danger;">Analogía Estructural</mark>

Imagina un sistema universitario:

* En la **Facultad de Ingeniería**, existe un estudiante con ID "Luis".
* En la **Facultad de Medicina**, también existe un estudiante con ID "Luis".

Ambos "Luis" coexisten sin conflicto porque pertenecen a espacios de nombres (facultades) distintos. Para referirnos a ellos sin ambigüedad, usamos su cualificación completa: `Ingeniería.Luis` vs `Medicina.Luis`.

En Python, cada módulo crea su propio namespace aislado automáticamente al ser importado.

***

### <mark style="color:yellow;">2. Mecanismos de Importación</mark>

Python ofrece dos estrategias principales para cargar código de un módulo al script actual. La elección afecta directamente a cómo se accede a los nombres y la seguridad del código.

#### <mark style="color:$danger;">A. Importación Completa (Cualificada)</mark>

Se utiliza la palabra clave `import` seguida del nombre del módulo.

```python
import math

# Acceso cualificado: namespace.funcion
print(math.sqrt(16))
```

* **Comportamiento:** Python carga el módulo `math` y lo asigna a una variable local llamada `math`. Todos los contenidos (funciones, constantes) residen **dentro** de ese objeto.
* **Ventaja:** Máxima seguridad contra colisiones. Sabemos exactamente de dónde viene cada función (`math.sqrt` es claramente distinta de una posible función local `sqrt`).

#### <mark style="color:$danger;">B. Importación Selectiva (Directa)</mark>

Se utiliza la sintaxis `from ... import ...` para extraer partes específicas del módulo e inyectarlas directamente en el namespace actual.

```python
from math import sqrt

# Acceso directo: funcion
print(sqrt(16)) 
```

* **Comportamiento:** La función `sqrt` se copia al ámbito global del script actual. Ya no es necesario usar el prefijo `math.`.
* **Ventaja:** Código más conciso.
* **Riesgo:** Posible colisión de nombres si ya existía una variable llamada `sqrt`.

***

### <mark style="color:yellow;">3. El Problema de las Colisiones de Nombres</mark>

La razón principal para preferir la importación cualificada (`import math`) sobre la selectiva es evitar la **sobrescritura silenciosa**.

**Caso de Estudio: El conflicto de `pi`**

```python
# 1. Definimos una variable local importante
pi = 3  # Valor entero para una lógica específica

# 2. Importamos pi desde el módulo matemático
from math import pi 

# 3. ¿Qué pasó con nuestra variable?
print(pi) 
# Salida: 3.141592... (La variable local fue sobrescrita sin aviso)
```

Si hubiéramos usado `import math`, tendríamos acceso a ambos valores simultáneamente:

* `pi`: Nuestra variable (3).
* `math.pi`: La constante matemática (3.14...).

***

### <mark style="color:yellow;">4. La Importación Comodín (Wildcard Import)</mark>

Existe una variante de la importación selectiva que usa un asterisco (`*`) para importar **todo** el contenido de un módulo.

```python
from math import *

print(sqrt(25))
print(sin(90))
print(pi)
```

#### <mark style="color:$danger;">Por qué se considera una Mala Práctica</mark>

Aunque parece conveniente para escribir menos, su uso está fuertemente desaconsejado en desarrollo profesional (salvo sesiones rápidas en consola interactiva) por dos razones críticas:

1. **Contaminación del Namespace:** Inyecta docenas o cientos de nombres desconocidos en tu script. Es muy probable que alguno de ellos colisione con tus variables locales.
2. **Pérdida de Trazabilidad:** Al leer el código, es imposible saber de dónde salió una función. ¿`sqrt` viene de `math`, de `numpy`, o es una función local? El código se vuelve ilegible y difícil de mantener.
