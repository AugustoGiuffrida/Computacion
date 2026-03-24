# Funciones

Las funciones son bloques de código encapsulados e independientes diseñados para realizar una tarea específica y reutilizable. En Python, se definen utilizando la palabra reservada `def`.

**Distinción importante :**
Desde la perspectiva formal de las ciencias de la computación:
* Un **parámetro** es la variable que se usa para recibir datos de entrada.
* Un **argumento** es el valor o dato real que se envía a la función cuando esta es *invocada*.

## 1. Definición y Llamada de Funciones

Para definir una función se especifica su nombre, seguido de paréntesis y dos puntos `:`. El cuerpo de la función debe estar obligatoriamente indentado.

```python
# Definición de la función (espera un parámetro 'nombre')
def saludar_estudiante(nombre):
    # Bloque de código interno
    print(f"Bienvenido al sistema, {nombre}.")

# Llamada a la función (se envía el argumento "Carlos")
saludar_estudiante("Carlos")
```

## 2. Argumentos Posicionales y de Palabra Clave (Keyword Arguments)

Al llamar a una función, Python permite enviar los argumentos de dos maneras principales:

1. **Argumentos Posicionales:** Son aquellos que se asignan a los parámetros basándose estrictamente en el **orden** en que fueron pasados.
2. **Argumentos de Palabra Clave (kwargs):** Se envían utilizando la sintaxis `clave = valor`. Al hacer esto, el orden en el que se pasan los argumentos deja de importar, ya que Python mapea los valores directamente por el nombre del parámetro.

```python
def registrar_nota(alumno, materia, calificacion):
    print(f"El alumno {alumno} obtuvo un {calificacion} en {materia}.")

# Llamada posicional (El orden es estricto)
registrar_nota("Carlos", "Álgebra", 8)

# Llamada con Keyword Arguments (El orden no importa)
registrar_nota(calificacion=9, alumno="Ana", materia="Física")
```

## 3. Argumentos por Defecto

Si se define un parámetro con un valor por defecto mediante el operador de asignación `=`, dicho parámetro se vuelve opcional al momento de llamar a la función. Si el usuario no provee un argumento para ese parámetro, Python utilizará el valor predeterminado.

```python
def configurar_idioma(idioma="Español"):
    print(f"El sistema está configurado en: {idioma}")

configurar_idioma("Inglés")  # Sobrescribe el valor por defecto
configurar_idioma()          # Al estar vacío, utiliza "Español"
```

## 4. Retorno de Valores (`return`)

Para permitir que una función devuelva un resultado al flujo principal del programa, se utiliza la sentencia `return`. Una vez que el intérprete ejecuta un `return`, la función finaliza inmediatamente, ignorando cualquier código que esté por debajo.
Si una función no posee un `return` explícito, Python retornará internamente el objeto `None`.

```python
def calcular_promedio(nota1, nota2):
    promedio = (nota1 + nota2) / 2
    return promedio

resultado_final = calcular_promedio(8, 10)
print(f"El promedio calculado es: {resultado_final}")
```


## 5. Argumentos Arbitrarios (`*args` y `**kwargs`)

Habrá escenarios en el diseño de software donde **no se sabrá de antemano cuántos argumentos** se pasarán a una función. Python resuelve esto mediante los operadores de *empaquetado* (packing) de variables: el asterisco simple `*` y el doble asterisco `**`.

### Argumentos Posicionales Arbitrarios (`*args`)
Si añades un `*` antes del nombre del parámetro, Python tomará todos los argumentos posicionales adicionales que se envíen y los **empaquetará internamente en una Tupla**.
*Se utiliza por convención el nombre `args`, pero el operador funcional real es el asterisco `*`.*

**Ejemplo:**
Supongamos que queremos una función que sume notas, pero un estudiante puede tener 2, 5 o 10 notas diferentes.

```python
def sumar_notas(*args):
    # 'args' ahora es una tupla que contiene todos los valores pasados.
    # Por ejemplo: (8, 9, 7, 10)
    total = 0
    for nota in args:
        total += nota
    return total

# Podemos llamar a la función con cualquier cantidad de argumentos posicionales
suma_1 = sumar_notas(8, 9)             # Pasamos 2 argumentos
suma_2 = sumar_notas(8, 9, 7, 10, 6)   # Pasamos 5 argumentos

print("Suma 1:", suma_1) # Salida: 17
print("Suma 2:", suma_2) # Salida: 40
```

### Argumentos de Palabra Clave Arbitrarios (`**kwargs`)
Si añades `**` antes del nombre del parámetro, Python tomará todos los argumentos de palabra clave (keyword arguments) adicionales que se envíen y los **empaquetará internamente en un Diccionario**, donde la clave es el nombre del parámetro y el valor es el dato asignado.

**Ejemplo:**
Supongamos que queremos crear un perfil de usuario, pero no sabemos qué atributos enviará el sistema (edad, dirección, carrera, etc.).

```python
def crear_perfil_estudiante(nombre, **kwargs):
    # 'nombre' es un parámetro posicional normal.
    # 'kwargs' captura el resto y crea un diccionario.
    print(f"Creando perfil para: {nombre}")
    
    # Iteramos sobre el diccionario empaquetado
    for clave, valor in kwargs.items():
        print(f" - {clave.capitalize()}: {valor}")

# Llamada a la función enviando múltiples keyword arguments no definidos previamente
crear_perfil_estudiante(
    "María Rodríguez", 
    carrera="Ingeniería en Sistemas", 
    semestre=4, 
    becada=True
)
```

**Salida de la ejecución:**
```text
Creando perfil para: María Rodríguez
 - Carrera: Ingeniería en Sistemas
 - Semestre: 4
 - Becada: True
```