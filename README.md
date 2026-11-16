# Coach UTPL Computación

Prototipo de **rutas de conocimiento actualizadas** para las asignaturas de la Carrera de Computación de la Universidad Técnica Particular de Loja (UTPL), con un tutor basado en **Generación Aumentada por Recuperación (RAG)** y retos de práctica.

Prueba de concepto del trabajo *RAG para entrenamiento activo de estudio acotado al temario universitario*, de la asignatura **Tecnologías Emergentes** (Unidad 5: Inteligencia Artificial).

**Demostración:** https://pabloc2a.github.io/coach-utpl-computacion/

## Problema

El software cambia rápido. Entre 2024 y 2025, la proporción de desarrolladores que usan o planean usar herramientas de IA pasó del 76 % al 84 % (Stack Overflow, 2025). Una guía didáctica lineal que se actualiza por periodo académico no muestra qué temas son fundamentos que no caducan, qué se usa hoy en la industria y qué ya está en desuso.

## Funciones

| Sección | Qué hace |
|---|---|
| Rutas | Muestra los temas de cada asignatura como un camino, al estilo de roadmap.sh. Cada tema se etiqueta como fundamento, vigente o emergente. La ruta incluye lo que se usa hoy en la industria, lo que está en desuso y un proyecto propuesto. |
| Asignaturas | Catálogo de las asignaturas por ciclo, con el avance del estudiante en cada ruta. |
| Tutor | Recupera fragmentos de las rutas, responde solo con ese material, cita la fuente y declara lo que está fuera de alcance. |
| Retos | Preguntas con vidas y puntos, inspiradas en Duolingo. Un tema se completa al aprobar su práctica con 4 de 5 aciertos. Cada error se explica y genera una pregunta de refuerzo. |
| Cómo funciona | Describe la indexación, la recuperación y la respuesta con fuente. |

## Funcionamiento

1. **Indexación.** 525 fragmentos: 343 temas y, por cada una de las 57 rutas, la industria actual, lo que está en desuso y el proyecto propuesto.
2. **Recuperación.** La consulta se normaliza (sin tildes y con raíces de palabra) y se puntúa con BM25.
3. **Respuesta con fuente.** Se construye solo con los fragmentos recuperados y cita su origen.

Como el conocimiento está en documentos, actualizar una ruta consiste en reemplazar su documento, sin reentrenar ningún modelo. Todo se ejecuta en el navegador; el avance se guarda en el almacenamiento local.

## Estructura

```
index.html                           Aplicación completa (HTML, CSS y JavaScript)
data/malla.json                      Asignaturas de la malla, por ciclo e itinerario
data/temario.json                    Temario referencial: 343 temas en 57 asignaturas
data/rutas.json                      Etiquetas de vigencia, industria actual, tecnologías en desuso y proyecto por asignatura
prompts/ai_studio_instrucciones.txt  Instrucciones de sistema usadas en Google AI Studio (Gemini)
```

## Alcance

- Las asignaturas provienen de la malla de la Carrera de Computación, modalidad presencial (UTPL).
- El temario y las etiquetas de vigencia son **referenciales**, con revisión de noviembre de 2026. En una implementación real se sustituyen por las guías didácticas oficiales, revisadas cada semestre por los docentes.

## Herramientas de IA utilizadas

- **Claude Code (Anthropic):** estructuración de los datos, programación del índice de recuperación y de la interfaz, y pruebas de cada función.
- **Google AI Studio (Gemini):** prueba del tutor RAG sin programación (ver `prompts/`).
