# 🧠 Analizador Léxico/Sintáctico — Proyecto de Compiladores

Intérprete completo de un lenguaje de programación personalizado, desarrollado en Python con interfaz gráfica. El proyecto implementa las fases clásicas de un compilador: análisis léxico, análisis sintáctico y análisis semántico.

---

## 📋 Descripción

El sistema permite escribir o cargar código fuente en un lenguaje propio (basado en una gramática definida con [Lark](https://github.com/lark-parser/lark)), analizarlo y ejecutarlo en tiempo real. Incluye una interfaz gráfica que muestra el árbol sintáctico, la tabla de símbolos, los tokens generados y la salida del programa.

El lenguaje soporta tipos de datos (`int`, `float`, `string`), operaciones aritméticas, manipulación de cadenas y un comando de impresión propio: `cangri(...)`.

---

## 🗂️ Estructura del proyecto

```
Proyecto-Compiladores-main/
│
├── Interprete.py          # Núcleo del intérprete: gramática, transformador y análisis semántico
├── Visor_Arbol.py         # Interfaz gráfica (Tkinter) para visualizar el análisis
├── gramatica.txt          # Definición formal de la gramática (formato Lark)
├── test.txt               # Archivo de prueba con ejemplos del lenguaje
├── testV3.txt             # Casos de prueba adicionales (incluyendo errores esperados)
└── definición de gramatica_anotado.pdf   # Documentación de la gramática
```

---

## 🔤 El lenguaje

### Tipos de datos
| Tipo     | Ejemplo                  |
|----------|--------------------------|
| `int`    | `int x = 5;`             |
| `float`  | `float pi = 3.14;`       |
| `string` | `string s = "hola";`     |

### Operadores aritméticos
| Operador | Descripción       |
|----------|-------------------|
| `+`      | Suma              |
| `-`      | Resta             |
| `*`      | Multiplicación    |
| `/`      | División          |
| `^`      | Potenciación      |

### Operaciones con cadenas
| Función / Operador         | Descripción                                 |
|----------------------------|---------------------------------------------|
| `#+`                       | Concatenación de strings                    |
| `n #* "texto"`             | Repetición de un string `n` veces           |
| `replace(s, buscar, nuevo)`| Reemplaza una subcadena                     |
| `trim(s)`                  | Elimina espacios al inicio y al final       |
| `sub(s, inicio, fin)`      | Extrae una subcadena                        |
| `to_string(expr_num)`      | Convierte un número a string                |

### Impresión
```
cangri(expr1, expr2, ...);   // Imprime en consola (equivalente a print)
cangri();                     // Imprime línea vacía
```

### Comentarios
```
// Esto es un comentario de línea
```

### Fin de instrucción
Toda instrucción termina con `;`. El fin del archivo se indica con `$`.

---

## 💡 Ejemplo de código

```
int a, b = 45;
string saludo = "Hola";

a = 6 + b;
cangri(saludo, " el valor es ", to_string(a));

cangri(3 #* "ja ");                        // ja ja ja
cangri(replace("hola mundo", "mundo", "compiladores"));
cangri(trim("   hola   "));
cangri(sub("compilador", 0, 5));
```

---

## 🖥️ Interfaz gráfica

La interfaz (`Visor_Arbol.py`) incluye:

- **Editor de código** — escritura o carga de archivos `.txt`
- **Panel de tokens** — lista todos los tokens generados en el análisis léxico
- **Árbol sintáctico** — visualización del árbol de derivación
- **Tabla de símbolos** — muestra variables declaradas, su tipo, valor e inicialización
- **Consola de salida** — resultado de la ejecución del programa
- **Mensajes de error** — errores léxicos, sintácticos y semánticos con número de línea y columna

---

## ⚙️ Requisitos

- Python 3.10 o superior
- Librería [Lark](https://github.com/lark-parser/lark)
- Tkinter (incluido en la instalación estándar de Python)

---

## 🚀 Instalación y uso

**1. Clonar el repositorio**
```bash
git clone https://github.com/tu-usuario/Proyecto-Compiladores.git
cd Proyecto-Compiladores
```

**2. Instalar dependencias**
```bash
pip install lark
```

**3. Ejecutar la interfaz gráfica**
```bash
python Visor_Arbol.py
```

**4. Ejecutar el intérprete desde código (sin interfaz)**
```python
from Interprete import Interprete

interprete = Interprete()
resultado = interprete.interpretar_archivo("test.txt")

print("¿Éxito?", resultado["ok"])
print("Mensajes:", resultado["mensajes"])
print("Símbolos:", resultado["simbolos"])
```

---

## 🔍 Manejo de errores

El intérprete detecta y reporta tres tipos de errores con su ubicación exacta (línea y columna):

| Tipo              | Ejemplo                                              |
|-------------------|------------------------------------------------------|
| **Léxico**        | Carácter no válido en el código fuente               |
| **Sintáctico**    | Falta de `;`, paréntesis sin cerrar, token inesperado|
| **Semántico**     | Variable no declarada, tipos incompatibles, división por cero, variable no inicializada, redeclaración |

---

## 🛠️ Tecnologías utilizadas

- **Python 3** — lenguaje principal
- **Lark** — generación del parser y árbol sintáctico (gramática EBNF)
- **Tkinter** — interfaz gráfica de escritorio
- **Threading** — análisis en hilo separado para no bloquear la UI
