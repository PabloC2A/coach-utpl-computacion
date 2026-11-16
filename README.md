# Coach UTPL Computación

Prototipo de asistente basado en **Generación Aumentada por Recuperación (RAG)** sobre la malla curricular de la Carrera de Computación de la Universidad Técnica Particular de Loja (UTPL), modalidad presencial.

Prueba de concepto del trabajo *RAG para entrenamiento activo de estudio acotado al temario universitario*, de la asignatura **Tecnologías Emergentes** (Unidad 5: Inteligencia Artificial).

**Demostración:** se abre desde GitHub Pages (enlace en la descripción del repositorio) o descargando `index.html` y abriéndolo en el navegador.

## Funciones

| Sección | Qué hace |
|---|---|
| Malla | Muestra los 9 ciclos, 54 asignaturas y 135 créditos. Al seleccionar una asignatura resalta su cadena completa de prerrequisitos y las asignaturas que habilita. |
| Ruta de aprendizaje | Presenta los temas de cada asignatura como un camino. Cada tema se marca como en estudio, completado u omitido, y se muestra el avance por asignatura y en la carrera. |
| Asistente RAG | Recupera fragmentos de la malla y del temario, responde con la fuente citada y declara cuando un dato no forma parte del material cargado. |
| Retos | Preguntas de opción múltiple con vidas y puntos. Un error se explica con su fuente y genera una pregunta de refuerzo. Un tema se completa al aprobar su práctica con 4 de 5 aciertos. |
| Cómo funciona | Describe el proceso de indexación, recuperación y generación fundamentada. |

## Funcionamiento

1. **Indexación.** La malla y el temario se dividen en 413 fragmentos (asignaturas, ciclos, reglas y temas), cada uno con su etiqueta de origen.
2. **Recuperación.** La consulta se normaliza (sin tildes, con raíces de palabra y ciclos en números romanos) y se puntúa con BM25 contra los fragmentos.
3. **Generación fundamentada.** La respuesta se construye solo con los fragmentos recuperados y con la cadena de prerrequisitos calculada sobre el grafo de la malla, y cita su fuente.

Todo se ejecuta en el navegador, sin servidor. El avance del estudiante se guarda en el almacenamiento local del navegador.

## Estructura

```
index.html                       Aplicación completa (HTML, CSS y JavaScript)
data/malla.json                  Malla estructurada: asignaturas, ciclos, créditos, prerrequisitos e itinerarios
data/temario.json                Temario referencial: 343 temas en 57 asignaturas
prompts/ai_studio_instrucciones.txt  Instrucciones de sistema usadas en Google AI Studio (Gemini)
```

## Fuentes y alcance

- **Malla:** infografía institucional de la malla curricular de la Carrera de Computación, modalidad presencial (UTPL). Los datos se verificaron contra sus totales: 54 asignaturas, 135 créditos y 15 créditos por ciclo.
- **Temario:** es **referencial**. Fue redactado para el prototipo porque la malla solo contiene los nombres de las asignaturas. En una implementación real se sustituye por las guías didácticas oficiales de cada asignatura.
- El prototipo no reemplaza al tutor académico: la validación oficial de la matrícula corresponde a la universidad.

## Herramientas de IA utilizadas

- **Claude Code (Anthropic):** estructuración de la malla en datos, programación del índice de recuperación, del grafo de prerrequisitos y de la interfaz, y pruebas de cada función.
- **Google AI Studio (Gemini):** prueba del asistente RAG sin programación, con la malla y el temario como contexto del sistema (ver `prompts/`).
