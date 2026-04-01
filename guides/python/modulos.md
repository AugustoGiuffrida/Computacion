# Arquitectura del Código

A medida que un proyecto crece, mantener todo el código en un único archivo se vuelve insostenible. Python aborda la escalabilidad mediante un sistema de **módulos** y **paquetes**, los cuales permiten dividir un programa en múltiples componentes, facilitando el mantenimiento y la reutilización del código.

## 1. ¿Qué es un Módulo?

En su definición más estricta, un módulo es un archivo fuente de Python. El nombre del archivo (sin la extensión `.py`) determina el nombre del módulo dentro del espacio de nombres del programa.

## 2. ¿Qué es un Paquete?

Un paquete es un directorio que agrupa varios módulos para evitar colisiones de nombres y organizar la arquitectura del proyecto. 

Para que el intérprete de Python reconozca formalmente a un directorio común del sistema operativo como un "paquete importable", tradicionalmente **debe contener un archivo especial llamado `__init__.py`**.

**Ejemplo:**
```text
mi_proyecto/
├── main.py
└── utilidades/                 # Esto es un Paquete
    ├── __init__.py             # Archivo de inicialización
    ├── calculos.py             # Módulo
    └── funciones_texto.py      # Módulo
```

### 2.1 La evolución histórica: ¿Es estrictamente necesario `__init__.py`?

Desde la versión 3.3 de Python (a través del PEP 420), **ya no es estrictamente obligatorio** incluir un archivo `__init__.py` para que una carpeta sea tratada como un paquete. Esto introdujo el concepto de *Namespace Packages* (Paquetes de Espacio de Nombres), permitiendo que un mismo paquete lógico esté distribuido en múltiples directorios físicos del disco.

Sin embargo, **es una práctica fuertemente recomendada seguir utilizándolo** por los siguientes motivos:
1.  Hace explícita la intención arquitectónica (cumpliendo el principio *Zen de Python*: "Explícito es mejor que implícito").
2.  Garantiza compatibilidad con herramientas de análisis estático (Linters), entornos de desarrollo (IDE) y frameworks de testing.
3.  Permite ejecutar código de inicialización y controlar la API pública del paquete.

## 3. ¿Qué es una libreria?
Se refiere a una colección de paquetes y módulos distribuidos conjuntamente para resolver un dominio de problemas específico (ej. `numpy`, `pandas`, `requests`).
