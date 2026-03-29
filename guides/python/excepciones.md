# Excepciones

En el desarrollo de software, es crucial distinguir entre dos tipos principales de errores: los **Errores de Sintaxis**, que ocurren durante la fase de compilación cuando el código viola las reglas gramaticales del lenguaje (evitando que el programa siquiera comience), y las **Excepciones**, que son eventos que ocurren durante tiempo de ejecución (Runtime), cuando el programa es sintácticamente correcto pero realiza una operación no válida.

Cuando ocurre un error en tiempo de ejecución (como dividir por cero o intentar abrir un archivo inexistente), se interrumpe el flujo normal del programa, instancia un objeto que representa ese error específico y lo "lanza" (raises). Si este objeto no es capturado y manejado por el programador, el programa colapsa (Crash) y el intérprete imprime un rastro de la pila (*Traceback*).

Para controlar este comportamiento y evitar el colapso del sistema, Python proporciona la estructura de control `try...except...else...finally`.

## 1. Bloques `try` y `except`

- **`try` (Intentar):** Define un ámbito de ejecución supervisado. Le indica a la Máquina Virtual de Python que ejecute el bloque de código contenido y que esté alerta ante cualquier objeto de excepción que pueda ser instanciado allí dentro.
- **`except` (Exceptuar/Capturar):** Si ocurre una excepción dentro del bloque `try`, el flujo de ejecución salta inmediatamente al bloque `except`. 

Por buenas prácticas, un bloque `except` nunca debería estar vacío o capturar errores genéricos sin justificación; debe diseñarse para interceptar clases de excepciones específicas.

**Ejemplo Práctico:**
```python
# Un bloque try supervisa las instrucciones susceptibles a fallar
try:
    dividendo = 10
    divisor = 0
    # Esta operación matemática es ilegal. Python instanciará un objeto ZeroDivisionError
    resultado = dividendo / divisor
    print("Esta línea nunca se ejecutará.")

except ZeroDivisionError:
    # Este bloque intercepta específicamente los errores de división por cero
    print("Error Crítico: Intento de división por cero detectado y neutralizado.")
except TypeError:
    # Se pueden encadenar múltiples except para diferentes escenarios
    print("Error de Tipo: Operación entre tipos de datos incompatibles.")
```

## 2. La cláusula `else` en Excepciones

La palabra reservada `else` puede acoplarse después de los bloques `except`. Su función es definir un bloque de código que **solo se ejecutará si el bloque `try` finalizó con éxito**, es decir, si no se levantó absolutamente ninguna excepción.

El bloque `try` debe contener estrictamente la línea de código que podría fallar, mientras que la lógica que depende de ese éxito debe ir en el `else`. Esto evita capturar accidentalmente excepciones de líneas de código que no pretendíamos supervisar.

**Ejemplo Práctico:**
```python
try:
    numero = int("15") # Conversión exitosa
except ValueError:
    print("El valor ingresado no es un número entero válido.")
else:
    # Solo ingresa aquí porque no hubo ValueError
    print(f"Conversión exitosa. El número multiplicado por 2 es: {numero * 2}")
```

## 3. La cláusula `finally`

El bloque `finally` se coloca al final de la estructura y contiene código que **garantiza su ejecución sin importar lo que haya sucedido**. Se ejecutará independientemente de si el bloque `try` fue exitoso, si ocurrió una excepción, o si la excepción fue capturada o no.

Se utiliza para cerrar conexiones a bases de datos, cerrar descriptores de archivos, o liberar bloqueos de memoria (locks), asegurando que el sistema operativo recupere los recursos incluso si el programa falla catastróficamente.

**Ejemplo Práctico:**
```python
try:
    print("Intentando establecer conexión con la base de datos...")
    # Simulación de un error durante la transacción
    resultado = 10 / 0 
except ZeroDivisionError:
    print("Fallo en la transacción de datos.")
finally:
    # Esta línea se ejecutará SIEMPRE.
    print("Cerrando la conexión a la base de datos de forma segura.")
```

## 4. Lanzar excepciones explícitamente (`raise`)

La palabra clave `raise` detiene la ejecución del bloque actual y **lanza manualmente una excepción**. Para usar `raise`, debemos instanciar un objeto de una clase de excepción (ya sea nativa de Python o creada por nosotros).

**Ejemplo Práctico:**
```python
def registrar_usuario(edad):
    if edad < 18:
        # Imponemos una restricción de negocio lanzando una excepción explícitamente
        raise ValueError("El sistema rechaza la operación: El usuario debe ser mayor de edad.")
    print("Usuario registrado exitosamente.")

try:
    registrar_usuario(15)
except ValueError as error_instanciado:
    # 'error_instanciado' es la variable que almacena el objeto de la excepción
    print(f"Operación abortada. Motivo: {error_instanciado}")
```

## 5. La Clase Base `Exception` y Jerarquía Orientada a Objetos

El sistema de manejo de errores de Python está basado en la Programación Orientada a Objetos (OOP). Todas las excepciones en Python son clases jerarquizadas.

En la cima de esta jerarquía se encuentra `BaseException` (que incluye eventos a nivel del sistema operativo como la interrupción del teclado `Ctrl+C`). Sin embargo, **todas las excepciones relacionadas con errores de lógica y programación heredan de la clase base `Exception`.**

* `Exception`
    * `ArithmeticError`
        * `ZeroDivisionError`
    * `LookupError`
        * `IndexError`
        * `KeyError`
    * `TypeError`
    * `ValueError`

Si en un bloque `except` capturamos la clase `Exception` estaremos interceptando *cualquier* error posible. Esto suele considerarse un "anti-patrón" de diseño (conocido como *pokemon exception handling*: "¡Atrápalos a todos!"), ya que enmascara errores imprevistos que deberían hacer fallar el programa durante la fase de desarrollo para poder corregirlos.

```python
try:
    lista = [1, 2, 3]
    # IndexError: Índice fuera de rango
    print(lista[10]) 
except Exception as e:
    # ESTO ES UNA MALA PRÁCTICA (si no está justificada)
    # Captura el IndexError, pero también capturaría un TypeError, un ValueError, etc.
    # Pierdes el control sobre qué está fallando realmente en tu código.
    print(f"Ocurrió un error inesperado de tipo: {type(e).__name__}")
```