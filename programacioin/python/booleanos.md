# Booleanos

En el desarrollo de software, la capacidad de tomar decisiones se basa en la evaluación de condiciones: ¿Es mayor de edad? ¿Está la lista vacía? ¿El usuario tiene permisos?

La respuesta a estas interrogantes binarias se representa mediante el tipo de dato **Booleano** (`bool`). Este tipo de dato es la unidad fundamental de la lógica computacional y el control de flujo.

***

### Los Valores: `True` y `False`

El tipo `bool` es estricto y finito; solo admite dos estados posibles:

1. **`True`**: Representa la afirmación, el encendido o el valor verdadero.
2. **`False`**: Representa la negación, el apagado o el valor falso.

#### Sensibilidad a Mayúsculas (Case Sensitivity)

Es un error sintáctico común escribir estos valores en minúsculas. En Python, la mayúscula inicial es obligatoria.

```python
sesion_activa = True   # Correcto
# sesion_activa = true # Error: Python buscará una variable llamada 'true'

print(f"Estado: {sesion_activa}")
print(f"Tipo: {type(sesion_activa)}")
```

**Salida:**

```
Estado: TrueTipo: <class 'bool'>
```

#### Palabras Reservadas

`True` y `False` son palabras clave reservadas del lenguaje (keywords). Esto implica que está prohibido utilizarlas como identificadores o nombres de variables. Intentar reasignarlas provocará un error de sintaxis inmediato.

```python
# Error de Sintaxis: no se puede asignar a True
True = 10
```

**Salida del error:**

```
SyntaxError: cannot assign to True
```

***

### Naturaleza Numérica de los Booleanos

Desde una perspectiva técnica interna, el tipo `bool` en Python es una **subclase** del tipo `int` (enteros). Esto significa que los booleanos se comportan como números en contextos aritméticos.

* **`True`** equivale numéricamente a **1**.<br>
* **`False`** equivale numéricamente a **0**.<br>

Esta característica permite realizar conversiones directas e incluso operaciones matemáticas (aunque esto último no se recomienda por legibilidad, es posible).

```python
# Conversión explícita a entero
valor_true = int(True)
valor_false = int(False)

print(f"True es: {valor_true}")
print(f"False es: {valor_false}")

# Aritmética Booleana (Demostración técnica)
suma_logica = True + True  # Equivale a 1 + 1
print(f"Resultado aritmético: {suma_logica}")
```

**Salida:**

```
True es: 1False es: 0Resultado aritmético: 2
```
