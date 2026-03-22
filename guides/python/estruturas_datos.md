# Introduccion sobre Estructuras de datos

En este documento exploraremos las colecciones de datos fundamentales en Python y las técnicas para la manipulación de cadenas de texto.
El objetivo es comprender no solo la sintaxis para utilizar estas herramientas, sino también su funcionamiento y en qué escenarios es más eficiente elegir una sobre otra.

## Estructuras de datos
Una estructura de datos es un formato especializado para organizar, procesar, recuperar y almacenar datos.

### 1.1 Listas

Las listas son colecciones ordenadas y mutables que permiten almacenar múltiples elementos. Cada elemento tiene una posición específica, denominada **índice**, que comienza en 0 para el primer elemento, 1 para el segundo, y así sucesivamente.

**Características y funcionamiento interno:**

- **Mutabilidad:** Las listas pueden modificarse después de su creación. Esto significa que puedes agregar, eliminar o actualizar elementos. Al ser mutables, cada operación de modificación (como `append`, `insert`, o asignar a un índice) desencadena ciertas verificaciones internas en Python para:
    - **Verificar la validez del índice:** Se comprueba que el índice usado para acceder o modificar esté dentro de los límites de la lista, evitando errores como `IndexError`.
    - **Mantener la integridad de la estructura:** Cuando se añaden elementos, Python puede necesitar reasignar memoria para expandir la lista. Esto implica mover datos y actualizar referencias para garantizar que la lista conserve su coherencia interna.
    - **Gestión de referencias:** Al modificar la lista, se actualizan las referencias a los objetos almacenados, asegurando que no haya fugas de memoria y que la información sea accesible de manera correcta.

- **Manejo de índices:** 
    - **Índices positivos:** Comienzan en 0, lo que permite acceder al primer, segundo, tercer elemento, etc. Por ejemplo, `lista[0]` devuelve el primer elemento.
    - **Índices negativos:** Permiten acceder a los elementos desde el final de la lista. Por ejemplo, `lista[-1]` devuelve el último elemento, `lista[-2]` el penúltimo, y así sucesivamente.
    - **Verificaciones de rango:** Cada vez que se accede a la lista mediante un índice, Python verifica que el índice esté dentro del rango permitido para evitar errores en tiempo de ejecución.

- **Uso recomendado:** Utiliza listas cuando necesites una colección de elementos que pueda cambiar durante la ejecución del programa, por ejemplo, para gestionar datos dinámicos, realizar operaciones de inserción o eliminación, o manipular secuencias de elementos de manera flexible.

- **Ejemplos:**

    ```python
    # Creación de una lista
    frutas = ["manzana", "banana", "cereza"]

    # Agregar un elemento al final
    frutas.append("naranja")  # Se realizan verificaciones internas para garantizar la consistencia

    # Modificar un elemento en una posición específica
    frutas[1] = "kiwi"  # 'banana' es reemplazada por 'kiwi'

    # Acceso a elementos mediante índices
    print("Primera fruta:", frutas[0])  # Acceso con índice positivo
    print("Última fruta:", frutas[-1])   # Acceso con índice negativo

    # Recorrer la lista mostrando índices y elementos
    for indice, fruta in enumerate(frutas):
        print(f"Fruta en el índice {indice}: {fruta}")
    ```
  
    ```python
  # Creación de una lista
  frutas = ["manzana", "banana", "cereza"]
    
  # Inserta 'mango' en el índice 1
  frutas.insert(1, 'mango')

  print(frutas)
  # Output: ["manzana", "mango", "banana", "cereza"]
  ```

### 1.2 Tuplas

Las tuplas son colecciones ordenadas e inmutables que, al igual que las listas, almacenan múltiples elementos y utilizan índices para su acceso. Sin embargo, una vez definidas, sus elementos no pueden modificarse.

**Características y ventajas:**

- **Inmutabilidad:**
  Una vez creada, la tupla no puede alterarse. Esto implica que:

    - No se pueden agregar, eliminar o modificar elementos.

    - No se realizan las verificaciones internas de integridad y actualización de memoria que son propias de las listas.

    - Esta inmutabilidad permite a Python optimizar el uso de memoria y mejorar la velocidad de acceso a los datos.

- **Manejo de índices:**

    - Al igual que las listas, los elementos de una tupla se acceden mediante índices positivos (empezando en 0) y negativos (para contar desde el final).

    - La inmutabilidad elimina la necesidad de verificaciones en operaciones de modificación, ya que no existen tales operaciones en las tuplas.

- **Uso recomendado:**
  Emplea tuplas cuando necesites garantizar que los datos permanezcan constantes durante la ejecución del programa, por ejemplo, para almacenar configuraciones fijas, coordenadas o cualquier conjunto de valores que no deban cambiar.

- **Ejemplo:**

    ```python
    # Creación de una tupla
    coordenadas = (15.5, 23.8)

    # Acceso a elementos mediante índices
    print("Coordenada x:", coordenadas[0])
    print("Coordenada y:", coordenadas[1])

    # Acceso utilizando índices negativos
    print("Última coordenada:", coordenadas[-1])

    # Intentar modificar una tupla genera error (descomentar la siguiente línea provocaría un TypeError)
    # coordenadas[0] = 20.0
    ```

### 1.3 Sets(Conjuntos)

Los conjuntos son colecciones desordenadas, no indexadas y mutables que no permiten elementos duplicados. Están diseñados matemáticamente para realizar operaciones de teoría de conjuntos (uniones, intersecciones, diferencias) de manera altamente eficiente.

**Características:**

- **Tablas Hash (Hash Tables):** A diferencia de las listas que almacenan elementos en ubicaciones de memoria contiguas o indexadas, los conjuntos en Python están implementados internamente como tablas hash.
- **Restricción de inmutabilidad en los elementos (Hashable):** Aunque el conjunto en sí es mutable (puedes agregar o quitar elementos), **los elementos que contiene deben ser inmutables** (como números, strings o tuplas). 
Python utiliza el valor del elemento para calcular un "hash" (una firma criptográfica/numérica) que determina exactamente dónde se almacenará en la memoria. 
Si un elemento pudiera cambiar (como una lista), su hash cambiaría, destruyendo la integridad de la tabla.

- **Ejemplo de Conjuntos:**

    ```python
    # Creación de conjuntos
    set_a = {"manzana", "banana", "cereza"}
    set_b = {"cereza", "naranja", "kiwi"}

    # Intentar añadir un duplicado es ignorado silenciosamente
    set_a.add("manzana") 

    # Operaciones matemáticas de conjuntos
    union = set_a.union(set_b)           # Todos los elementos únicos de ambos
    interseccion = set_a.intersection(set_b) # Solo los elementos en común ('cereza')
    diferencia = set_a.difference(set_b)     # Elementos en set_a que no están en set_b
    ```

### 1.4 Diccionarios

Los diccionarios son colecciones mutables de pares clave-valor (key-value).

**Características:**

- **Mapeo de Hash (Hash Maps):**
  Al igual que los sets, los diccionarios utilizan tablas de hash. La diferencia es que el cálculo del hash se aplica únicamente a la **clave**, la cual actúa como un puntero hacia el **valor** asociado.
- **Restricciones de Claves y Valores:**
  Las claves deben ser de un tipo de dato inmutable y único (hashable). Si se intenta asignar un valor a una clave que ya existe, el valor anterior es sobrescrito. Por otro lado, los valores asociados no tienen ninguna restricción: pueden ser de cualquier tipo (listas, otros diccionarios, objetos, etc.).

- **Ejemplo de Diccionarios:**

    ```python
    # Creación de un diccionario
    estudiante = {
        "nombre": "Ana",
        "edad": 22,
        "materias": ["Python", "OOP"]
    }

    # Acceso a valores mediante su clave
    print(estudiante["nombre"])

    # Modificar un valor existente o agregar un nuevo par clave-valor
    estudiante["edad"] = 23
    estudiante["promedio"] = 9.5

    # Obtener todas las claves o todos los valores
    claves = estudiante.keys()
    valores = estudiante.values()
    ```

---

## 2. Manipulación de Strings (Cadenas de Texto)

Al comprender que los `strings` en Python son arreglos inmutables de caracteres Unicode, se deduce que no podemos modificar el objeto original en memoria. Sin embargo, Python proporciona métodos integrados (built-in methods) que procesan la cadena original y retornan un **nuevo objeto string** con las modificaciones solicitadas.

### 2.1 Métodos de Transformación y Búsqueda

- `strip()`: Retorna una nueva cadena eliminando los espacios en blanco (o caracteres especificados) al inicio y al final.
- `upper()` y `lower()`: Retornan una nueva cadena con todos los caracteres en mayúsculas o minúsculas, respectivamente.
- `replace(old, new)`: Busca un patrón específico y lo reemplaza por uno nuevo, retornando la cadena resultante.
- `split(separador)`: Analiza la cadena y la divide en múltiples subcadenas basándose en un separador, retornando una **lista** con los fragmentos.
- `join(iterable)`: Es el operador inverso a `split`. Toma un iterable (como una lista de strings) y los une en una sola cadena, utilizando el string original como separador.

- **Ejemplo Práctico:**

    ```python
    texto_sucio = "   Python es genial, Python es rapido   "
    
    # Limpieza y transformación encadenada
    texto_limpio = texto_sucio.strip().replace("Python", "OOP")
    print(texto_limpio) # Salida: "OOP es genial, OOP es rapido"

    # Separación en una lista
    palabras = texto_limpio.split(", ") # ['OOP es genial', 'OOP es rapido']

    # Unión eficiente de cadenas
    texto_unido = " | ".join(palabras)   # "OOP es genial | OOP es rapido"
    ```
