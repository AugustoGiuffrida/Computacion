# Glosario

## 1. Arboles
Un árbol es una estructura de datos jerárquica y no lineal compuesta por nodos conectados entre sí. 

### Conceptos fundamentales de la estructura:

* Nodo: Cada elemento del árbol que contiene información (como una variable, un número o un operador).
* Raíz (Root): El nodo superior del que parten todos los demás. En Python, la raíz representa el programa completo o un módulo.
* Padres e Hijos: Un nodo "padre" tiene conexiones hacia nodos inferiores llamados "hijos". Por ejemplo, en una operación `x = 5 + 3`, el nodo del operador `+` es padre de los nodos **5** y **3**.
* Hojas (Leaves): Los nodos finales que no tienen hijos; suelen ser los valores literales o nombres de variables.

```mermaid
flowchart TD;
%% Definición de la paleta de colores
    classDef raiz fill:#ffcdd2,stroke:#c62828,stroke-width:2px,color:#000;
    classDef intermedio fill:#bbdefb,stroke:#1565c0,stroke-width:2px,color:#000;
    classDef hoja fill:#c8e6c9,stroke:#2e7d32,stroke-width:2px,color:#000;

%% Nodos con etiquetas descriptivas integradas (se usa <br/> para el salto de línea)
    Raiz("<b>Raíz</b><br/>( = )"):::raiz --> Hoja1("<b>Hoja</b><br/>( resultado )"):::hoja
    Raiz --> NodoMult("<b>Nodo Padre</b><br/>( * )"):::intermedio

    NodoMult --> Hoja2("<b>Hoja</b><br/>( 5 )"):::hoja
    NodoMult --> NodoSuma("<b>Nodo Padre</b><br/>( + )"):::intermedio

    NodoSuma --> Hoja3("<b>Hoja</b><br/>( 2 )"):::hoja
    NodoSuma --> Hoja4("<b>Hoja</b><br/>( 3 )"):::hoja
```
