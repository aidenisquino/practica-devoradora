
## 📝 Resumen de Aprendizaje: Fundamentos y Diseño en LaTeX

### 1. Gestión de Espacios y Columnas
* **Crear variables de medida:** Se utiliza `\newlength{\nombre}` para crear una variable en blanco que almacenará una medida (por ejemplo, el ancho de una columna).
* **Asignar valores:** Con `\setlength{\nombre}{valor}` le damos un tamaño a esa variable. Es muy útil usar proporciones relativas, como `0.23\textwidth` (el 23% del ancho total del texto de la página), para que el diseño sea adaptable.
* **Paquete `paracol`:** Excelente para hacer documentos a dos (o más) columnas. Se configura la separación con `\setlength{\columnsep}{...}` y la proporción de cada columna con `\columnratio{izq}[der]`.

### 2. Comandos Personalizados (Macros)
* Muchas plantillas de CV o documentos avanzados usan comandos inventados por el autor (como `\simpleheader` o `\infobubble`) para simplificar el código.
* **Cómo se crean:** Se usa `\newcommand{\nombrecomando}[cantidad_parametros]{código}`. Los parámetros se representan con `#1`, `#2`, etc.
* Para replicar elementos gráficos complejos (como íconos dentro de círculos de color), se suele combinar el poder de dibujo del paquete **`tikz`** con librerías de íconos como **`fontawesome5`**.

### 3. Párrafos y Sangrías (Indentation)
* **La regla de oro:** En LaTeX, el comando `\paragraph{}` **es un título de sección**, no sirve para formatear texto normal. Además, por defecto, el primer párrafo después de un título *nunca* lleva sangría.
* **Tamaño de sangría:** Se define globalmente con `\setlength{\parindent}{20pt}`.
* **Solución global (Recomendada):** Agregar el paquete `\usepackage{indentfirst}` en el preámbulo para que todos los primeros párrafos tengan sangría automáticamente.
* **Solución manual:** Usar el comando `\indent` justo antes de la primera palabra del párrafo.

### 4. Alineación del Texto
* **Justificado por defecto:** LaTeX justifica el texto automáticamente de forma profesional. Esta es la mejor opción para ensayos académicos.
* **Entorno `flushleft`:** Alinea el texto rígidamente a la izquierda. **Atención:** usar este entorno desactiva la justificación y elimina automáticamente todas las sangrías del texto que esté dentro de él.

### 5. Entornos vs. Grupos (El control del alcance / Scope)
* **Entornos (`\begin{...}` y `\end{...}`):** Son bloques inteligentes y semánticos (listas, tablas, alineaciones) que aplican reglas complejas y tienen validación de errores.
* **Grupos (`\begingroup` y `\endgroup` o llaves `{ }`):** Son contenedores "crudos" que sirven exclusivamente para aislar cambios de formato (como un cambio de color o tamaño de letra) y evitar que afecten al resto del documento.
* **El detalle crucial del Párrafo (`\par`):** Si dentro de un grupo aplicas comandos de nivel de párrafo (como `\centering`, `\raggedright` o cambios de tamaño), **debes incluir una línea en blanco (o el comando `\par`) antes del `\endgroup`**. Si no lo haces, el grupo se cierra, la regla se destruye, y LaTeX armará el texto con el formato normal del documento, ignorando tu comando.

Aquí tienes un resumen de los conceptos básicos sobre cómo crear listas en LaTeX, basándonos en la guía de Overleaf y excluyendo las secciones de personalización avanzada (como el uso de contadores o el paquete `enumitem`):

### 6. Tipos básicos de listas
LaTeX ofrece tres entornos nativos para crear listas. En todos ellos, cada elemento nuevo dentro de la lista se declara obligatoriamente con el comando `\item`. 
* **Listas con viñetas (no ordenadas): Entorno `itemize`**
    Se utiliza para crear listas donde el orden no es relevante. Por defecto, cada elemento está precedido por un punto negro o viñeta.
    ```latex
    \begin{itemize}
      \item Primer elemento de la lista.
      \item Segundo elemento.
    \end{itemize}
    ```

* **Listas numeradas (ordenadas): Entorno `enumerate`**
    Se usa cuando el orden importa (como pasos a seguir). LaTeX enumera los elementos de forma automática empezando desde el 1.
    ```latex
    \begin{enumerate}
      \item Primer paso.
      \item Segundo paso.
    \end{enumerate}
    ```

* **Listas de descripciones: Entorno `description`**
    Ideal para crear glosarios, diccionarios o listas de términos y definiciones. El comando `\item` toma un argumento opcional entre corchetes `[...]` que representa la palabra a describir (LaTeX la imprimirá en negrita al inicio de la línea).
    ```latex
    \begin{description}
      \item[LaTeX] Un sistema de preparación de documentos.
      \item[Overleaf] Un editor colaborativo en línea.
    \end{description}
    ```

*(Nota: En cualquiera de estos tres entornos, es posible cambiar temporalmente el símbolo o número de un solo renglón escribiendo algo distinto entre corchetes justo después del ítem, por ejemplo: `\item[*]`).*

### 7. Listas Anidadas (Sub-listas)
LaTeX permite insertar una lista dentro de otra de manera nativa hasta **un máximo de 4 niveles de profundidad** (sin requerir paquetes extra de configuración). 
Puedes anidar listas del mismo tipo o combinar diferentes entornos (por ejemplo, poner un bloque `itemize` dentro de un ítem de un `enumerate`).

**Comportamiento automático al anidar:**
* **En `itemize`:** El símbolo de la viñeta cambia por sí solo según el nivel en el que te encuentres (ej. nivel 1: punto negro, nivel 2: guion, nivel 3: asterisco).
* **En `enumerate`:** El estilo del número se adapta al nivel de profundidad para no confundir al lector (ej. nivel 1: números `1.`, nivel 2: letras minúsculas `(a)`, nivel 3: números romanos `i.`).

**Ejemplo de estructura anidada:**
```latex
\begin{enumerate}
  \item Título principal (Nivel 1, número 1)
  \begin{itemize}
    \item Sub-punto (Nivel 2, viñeta normal)
    \begin{itemize}
      \item Detalle extra (Nivel 3, cambia la viñeta)
    \end{itemize}
  \end{itemize}
  \item Siguiente título principal (Nivel 1, número 2)
\end{enumerate}
```

## 🧮 Resumen: Expresiones Matemáticas en LaTeX

Existen dos modos principales para escribir matemáticas, dependiendo de cómo quieras que se vea la ecuación en la hoja.

### 1. Modo en línea (Inline Math Mode)
Se utiliza cuando quieres que la fórmula matemática fluya naturalmente **dentro del mismo párrafo** de texto, sin romper la oración.

* **¿Cómo se declara?** Tienes tres opciones (todas hacen exactamente lo mismo, puedes elegir tu favorita):
    1.  `$ ... $` (Es la más rápida y la favorita de la mayoría de los usuarios).
    2.  `\( ... \)` (Es el estándar recomendado oficialmente por LaTeX moderno).
    3.  `\begin{math} ... \end{math}` (Es válida, pero casi nadie la usa por ser muy larga).
* **Ejemplo en código:** `La ecuación de la energía es $E=mc^2$ según Einstein.`
* **Resultado visual:** La ecuación de la energía es $E=mc^2$ según Einstein.

### 2. Modo de visualización (Display Math Mode)
Se utiliza para ecuaciones importantes o largas que necesitan destacar. LaTeX sacará la ecuación del texto, la colocará en una **línea nueva, la centrará** y ajustará el tamaño para que sea más legible.

* **¿Cómo se declara?** Depende de si quieres que la ecuación esté numerada o no:
    * **Ecuaciones sin numerar:**
        1.  `\[ ... \]` (La forma más recomendada).
        2.  `\begin{displaymath} ... \end{displaymath}`.
    * **Ecuaciones con numeración automática:**
        1.  `\begin{equation} ... \end{equation}`. Esto colocará un número (por ejemplo, "(1)") en el margen derecho, lo cual es vital en ensayos académicos para referenciar la fórmula más adelante.
        2.  *Nota:* Si usas `\begin{equation*}` (con asterisco), le quitas la numeración, pero necesitas tener cargado el paquete `amsmath` en tu preámbulo.
* **Ejemplo en código:** `El Teorema de Pitágoras dicta que:`
    `\[ x^2 + y^2 = z^2 \]`
* **Resultado visual:** El Teorema de Pitágoras dicta que:
    $$x^2 + y^2 = z^2$$
  
packages:

- fontawesome: permite añadir símbolos de diferentes empresas o dibujitos que permiten hacer el texto más cool
- tikz: permite crear elementos gráficos mediante vectores
