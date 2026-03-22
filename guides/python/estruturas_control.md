# Estructuras de Control

Por defecto, el intérprete de Python ejecuta las instrucciones de un script de forma estrictamente secuencial (de arriba hacia abajo). Las estructuras de control son bloques sintácticos que permiten alterar este flujo de ejecución natural, permitiendo que el programa tome decisiones dinámicas (bifurcaciones) o repita bloques de código (iteraciones) en función de la evaluación de expresiones lógicas.

## 1 Estructuras de Decisión

Las estructuras de decisión evalúan una expresión y determinan el camino que tomará la ejecución basándose en el resultado booleano (`True` o `False`) de dicha expresión.

**Sentencias Condicionales:**

- **`if`:** Es la estructura base. Evalúa una condición matemática o lógica. Si el resultado es `True`, se ejecuta el bloque de código que se encuentra indentado debajo de la declaración. Si es `False`, el bloque se omite.
- **`elif`:** Abreviatura de *else if*. Se utiliza para evaluar condiciones alternativas y mutuamente excluyentes si la condición del `if` original (y cualquier `elif` previo) resultó ser falsa. Python evaluará los `elif` en orden descendente y ejecutará únicamente el bloque del primero que resulte verdadero.
- **`else`:** Actúa como la rama de ejecución por defecto (el caso base). Captura cualquier escenario que no haya cumplido ninguna de las condiciones anteriores. No requiere evaluar una condición explícita.

**Aspectos Críticos de Diseño en Python:**

- **La Indentación es Semántica:** A diferencia de lenguajes de la familia C que utilizan llaves `{}` para delimitar qué sentencias pertenecen al condicional, Python utiliza exclusivamente la indentación (espacios en blanco). Si el bloque de código no está correctamente indentado, el intérprete lanzará un `IndentationError`.
- **Operadores Lógicos (`and`, `or`, `not`):** Permiten combinar múltiples expresiones relacionales en una sola evaluación compuesta.
- **La sentencia `pass`:** En Python, los bloques de código no pueden estar vacíos algorítmicamente. Si por razones de diseño arquitectónico se necesita escribir un condicional pero aún no se implementará su lógica, se debe utilizar la palabra reservada `pass` (una operación nula) para evitar un error de sintaxis.

**Ejemplo:**

```python
edad = 20
tiene_licencia = True

if edad >= 18 and tiene_licencia:
    print("El usuario es apto para conducir.")
    
    # Condicional anidado (Un if dentro de otro if)
    if edad < 21:
        print("Precaución: Conductor principiante (menor de 21 años).")
        
elif edad >= 18 and not tiene_licencia:
    print("El usuario tiene la edad, pero debe tramitar su licencia.")
else:
    print("El usuario no cumple con los requisitos mínimos de edad.")
```

**Expresiones Condicionales (Operador Ternario):**
Python permite sintetizar un bloque `if...else` sencillo en una sola línea de código. Esta estructura devuelve un valor en lugar de ejecutar sentencias aisladas, lo que resulta altamente eficiente para asignaciones dinámicas.

```python
# Sintaxis: [valor_si_true] if [condicion] else [valor_si_false]
numero = 10
estado = "Positivo" if numero > 0 else "Negativo o Cero"
```

---

## 2 Estructuras Repetitivas (Bucles)

Las estructuras repetitivas permiten que la Máquina Virtual de Python ejecute un mismo bloque de código de forma iterativa, reduciendo la redundancia de código y permitiendo el procesamiento de colecciones de datoss.

### Bucle `while`

El bucle `while` se utiliza cuando **no se conoce a priori la cantidad exacta de iteraciones** que deben realizarse.

- **Concepto:** Ejecuta repetidamente un bloque de código mientras la condición booleana evaluada en su cabecera resulte ser verdadera (`True`).
- **Control de Estado:** Es imperativo que dentro del bloque del bucle exista una operación lógica que altere el estado de la variable evaluada en la condición. Si la condición nunca cambia a `False`, se producirá un **bucle infinito**, consumiendo los recursos de la CPU hasta que el proceso sea forzado a detenerse.

```python
# Ejemplo de Bucle While
contador = 0
while contador < 5:
    print("Iteración número:", contador)
    contador += 1  # Operador de asignación (crucial para evitar bucle infinito)
```

### Bucle `for`

A diferencia de lenguajes como C o Java, donde un bucle `for` se define mediante un contador aritmético, el bucle `for` en Python funciona estrictamente como un **iterador**. Está diseñado para recorrer secuencialmente los elementos de un objeto iterable (como Listas, Tuplas, Strings, Sets o Diccionarios).

- **Parámetros comunes:** Requiere una variable de iteración que, en cada ciclo del bucle, tomará automáticamente el valor del siguiente elemento en la secuencia, hasta que la colección se agote.
- **La función `range()`:** Cuando se necesita iterar un número específico de veces sin depender de una colección preexistente, se utiliza el generador integrado `range()`. Retorna una secuencia de números (por defecto comenzando en 0 y con incrementos de 1).

```python
# Iterando sobre una colección (Lista)
nombres = ["Ana", "Luis", "Carlos"]
for nombre in nombres:
    print(f"Procesando usuario: {nombre}")

# Iterando un número específico de veces con range()
for i in range(3):  # Genera la secuencia 0, 1, 2
    print("Ciclo:", i)
```

### Sentencias de Control de Flujo Interno

Dentro de cualquier bucle (`while` o `for`), el flujo puede ser alterado abruptamente utilizando sentencias de control específicas:

- **`break`:** Interrumpe y finaliza el bucle inmediatamente, sin importar si la condición del `while` seguía siendo verdadera o si quedaban elementos en el iterable del `for`. El intérprete salta a la primera línea de código fuera del bucle.
- **`continue`:** Detiene únicamente la iteración actual. El código restante dentro del bloque se omite en ese ciclo, y el intérprete salta directamente a la evaluación de la siguiente iteración.

```python
for num in range(1, 10):
    if num == 3:
        continue # Se salta el número 3 y pasa directo al 4
    if num == 6:
        break    # Corta el bucle por completo al llegar al 6
    print(num)   # Salida: 1, 2, 4, 5
```

#### La cláusula `else` en los Bucles (Particularidad de Python)

A diferencia de la mayoría de los lenguajes, Python permite adjuntar una cláusula `else` al final de un bucle `for` o `while`.
El bloque de código dentro del `else` **solo se ejecutará si el bucle finaliza de manera natural** (es decir, cuando la condición del `while` se vuelve falsa, o cuando el `for` agota todos sus elementos). Si el bucle es interrumpido artificialmente por una sentencia `break`, el bloque `else` es ignorado.

```python
objetivo = 5
for i in range(3): # El iterador solo llega a 2
    if i == objetivo:
        print("Objetivo encontrado.")
        break
else:
    # Este bloque se ejecuta porque el bucle terminó sin encontrar un 'break'
    print("El bucle iteró sobre todos los elementos, pero no encontró el objetivo.")
```