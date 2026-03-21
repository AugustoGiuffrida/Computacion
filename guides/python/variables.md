# Variables y Tipos de Datos en Python

En este documento exploraremos en detalle cómo Python almacena la información, cómo maneja los espacios de memoria y cuáles son los tipos de datos integrados (built-in) que el lenguaje proporciona para modelar problemas del mundo real.

## 1. Variables: Referencias y Funcionamiento Interno

En Python, **una variable es una referencia (un puntero)** a un objeto que reside en la memoria. Cuando se asigna un valor a una variable, Python crea un objeto en memoria y hace que la variable apunte a ese objeto.

**Características principales:**
* Las variables no están fijadas a un tipo de dato específico. Pueden cambiar de tipo si se les reasigna un objeto diferente.
* Las variables `Edad` y `edad` apuntan a espacios de memoria y objetos completamente distintos (Case-Sensitive).

**Ejemplo **
```python
# Se crea un objeto de tipo entero con el valor 5 en memoria.
# La etiqueta 'x' se asocia a ese espacio de memoria.
x = 5       

# Tipado dinámico en acción:
# Ahora se crea un objeto de tipo cadena (str) y 'x' cambia su referencia hacia él.
# El objeto anterior (5) quedará a merced del recolector de basura si no hay otra variable apuntándolo.
x = "Hola"  

# Asignación múltiple: Python permite asignar valores a múltiples referencias en una sola línea
a, b, c = "Manzana", "Banana", "Cereza"
```

## 2. Tipos de Datos

En Python, los datos se clasifican fundamentalmente en **Inmutables** (no pueden cambiar su estado interno una vez creados en memoria) y **Mutables** (pueden ser modificados in-place).

Para conocer el tipo de clase del objeto al que apunta una variable, se recomienda utilizar la función `type()`.

### 2.1 Números
Python admite tres tipos principales de datos numéricos. Son objetos inmutables, lo que significa que al realizar una operación aritmética, no se modifica el objeto original, sino que se crea uno nuevo en memoria.

* **`int` (Enteros):** Números enteros, positivos o negativos, sin parte decimal.
* **`float` (De punto flotante):** Números reales que contienen una parte fraccionaria.
* **`complex` (Complejos):** Números con una parte real y una parte imaginaria, donde la parte imaginaria se denota con una `j`.

**Ejemplo:**
```python
x = 10           # int
y = 3.14         # float
z = -35.59e100   # float (Notación científica)
c = 3 + 5j       # complex

print(type(x))   # Salida: <class 'int'>
```


### 2.2 Cadenas de Texto (Strings)
Las cadenas de texto (tipo `str`) en Python son secuencias inmutables de caracteres Unicode. Esto permite soportar múltiples lenguajes y símbolos matemáticos de forma nativa. 

Al ser tratadas como "arreglos" (arrays) se puede acceder a elementos individuales utilizando índices (empezando desde 0).

**Características principales:**
* **Multilínea:** Se pueden definir usando comillas triples (`"""` o `'''`).
* **Slicing (Rebanado):** Permite extraer sub-cadenas especificando un índice de inicio y uno de fin `[inicio:fin]`.
* **F-Strings (Cadenas con formato):** Permiten incrustar expresiones y variables directamente dentro de la cadena usando el prefijo `f` y llaves `{}`.

**Ejemplo:**
```python
texto = "Universidad"

# Acceso por índice
primer_letra = texto[0]      # 'U'

# Slicing (Extraer desde el índice 0 hasta el 3, sin incluir el 3)
prefijo = texto[0:3]         # 'Uni'

# F-Strings para interpolación de variables
año = 2024
mensaje = f"Inicio del ciclo lectivo {año}"
print(mensaje)               # Salida: Inicio del ciclo lectivo 2024
```

### 2.3 Booleanos
El tipo `bool` representa uno de dos valores lógicos: `True` (Verdadero) o `False` (Falso). En Python, los booleanos son en realidad una subclase de los enteros (`int`), donde `True` equivale a 1 y `False` equivale a 0 internamente.

Casi cualquier valor en Python puede ser evaluado como un booleano utilizando la función `bool()`. Esto introduce el concepto de valores **"Truthy"** (evalúan a verdadero) y **"Falsy"** (evalúan a falso).

* **Valores Falsy:** Colecciones vacías (como `[]`, `()`, `""`, `{}`), el número `0`, y el objeto especial `None`.
* **Valores Truthy:** Cualquier cadena que no esté vacía, cualquier número distinto de cero, y cualquier colección que contenga elementos.

**Ejemplo:**
```python
es_estudiante = True
es_graduado = False

# Evaluación de Truthy y Falsy
print(bool("Hola"))   # True, porque la cadena no está vacía
print(bool(0))        # False, porque es el número cero
print(bool(""))       # False, porque es una cadena vacía
print(bool([]))       # False, porque es una lista vacía
```

### 2.4 Casting (Conversión de Tipos)
Habrá ocasiones en las que será necesario especificar o transformar explícitamente el tipo de un dato, un proceso conocido como **Casting**. Esto se logra utilizando funciones constructoras integradas correspondientes a la clase del objeto deseado:

* `int()`: Construye un número entero a partir de un entero, un flotante (truncando los decimales) o una cadena de texto (si representa un número entero válido).
* `float()`: Construye un número flotante a partir de un entero, un flotante o un texto.
* `str()`: Construye una cadena de texto a partir de una amplia variedad de tipos de datos.

**Ejemplo:**
```python
a = int(2.8)     # 'a' será el entero 2 (truncamiento, no redondeo)
b = float("3")   # 'b' será el flotante 3.0
c = str(3.0)     # 'c' será la cadena de texto "3.0"