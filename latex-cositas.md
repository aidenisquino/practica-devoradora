¡Por supuesto! Es una idea genial. Tener unos apuntes limpios les va a salvar mucho tiempo cuando estén escribiendo sus documentos finales. 

Aquí tienen un resumen estructurado con todo lo que hemos explorado hasta ahora, listo para que lo copien y peguen en su documento de notas:

---

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

packages:

- fontawesome: permite añadir símbolos de diferentes empresas o dibujitos que permiten hacer el texto más cool
- tikz: permite crear elementos gráficos mediante vectores
