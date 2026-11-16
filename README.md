# Coach UTPL Computación

Prototipo de **rutas de conocimiento actualizadas** para las asignaturas de la Carrera de Computación de la Universidad Técnica Particular de Loja (UTPL), con un tutor basado en **Generación Aumentada por Recuperación (RAG)** y retos de práctica.

Prueba de concepto del trabajo *RAG para entrenamiento activo de estudio acotado al temario universitario*, de la asignatura **Tecnologías Emergentes** (Unidad 5: Inteligencia Artificial).

**Demostración:** https://pabloc2a.github.io/coach-utpl-computacion/

## Problema

El software cambia rápido. Entre 2024 y 2025, la proporción de desarrolladores que usan o planean usar herramientas de IA pasó del 76 % al 84 % (Stack Overflow, 2025). Una guía didáctica lineal que se actualiza por periodo académico no muestra qué temas son fundamentos que no caducan, qué se usa hoy en la industria y qué ya está en desuso.

## Funciones

| Sección | Qué hace |
|---|---|
| Bienvenida | Al abrir la página, pregunta el nombre, el ciclo y, desde el ciclo VI, el itinerario. Muestra las asignaturas del ciclo con sus unidades y lecciones. El perfil se guarda solo en el navegador. |
| Rutas | Muestra cada asignatura como un camino de unidades y lecciones, al estilo de roadmap.sh y Duolingo. Las lecciones se reparten en un plan de 16 semanas, la duración de clases de un ciclo de cinco meses. Cada unidad se etiqueta como fundamento, vigente o emergente y termina en una práctica. La ruta incluye lo que se usa hoy en la industria, lo que está en desuso y un proyecto final. |
| Asignaturas | Catálogo de las asignaturas por ciclo, con el avance del estudiante en cada ruta. |
| Tutor | Recupera fragmentos de las rutas, responde solo con ese material, cita la fuente y declara lo que está fuera de alcance. |
| Retos | Preguntas con vidas y puntos, inspiradas en Duolingo. Una unidad se aprueba con 4 de 5 aciertos en su práctica, y sus lecciones quedan como estudiadas. Cada error se explica y genera una pregunta de refuerzo. |
| Cómo funciona | Describe la indexación, la recuperación y la respuesta con fuente. |

## Funcionamiento

1. **Indexación.** 533 fragmentos: 351 temas (unidades) con 1774 subtemas (lecciones) y, por cada una de las 57 rutas, la industria actual, lo que está en desuso y el proyecto propuesto.
2. **Recuperación.** La consulta se normaliza (sin tildes y con raíces de palabra) y se puntúa con BM25.
3. **Respuesta con fuente.** Se construye solo con los fragmentos recuperados y cita su origen.

Como el conocimiento está en documentos, actualizar una ruta consiste en reemplazar su documento, sin reentrenar ningún modelo. Todo se ejecuta en el navegador; el avance se guarda en el almacenamiento local.

## Estructura

```
index.html                           Aplicación completa (HTML, CSS y JavaScript)
data/malla.json                      Asignaturas de la malla, por ciclo e itinerario
data/temario.json                    Temario referencial: 351 unidades en 57 asignaturas
data/subtemas.json                   1774 lecciones y el referente académico de cada unidad
data/referentes.json                 Clases de Harvard CS50 usadas como referente, con su enlace
data/rutas.json                      Etiquetas de vigencia, industria actual, tecnologías en desuso y proyecto por asignatura
prompts/ai_studio_instrucciones.txt  Instrucciones de sistema usadas en Google AI Studio (Gemini)
```

## Alcance

- Las asignaturas provienen de la malla de la Carrera de Computación, modalidad presencial (UTPL).
- El temario y las etiquetas de vigencia son **referenciales**, con revisión de noviembre de 2026. En una implementación real se sustituyen por las guías didácticas oficiales, revisadas cada semestre por los docentes.

## Referentes académicos

83 temas toman como referente las clases de los cursos abiertos de Harvard CS50, verificadas en sus sitios oficiales. Cada tema enlaza a su clase:

| Curso de Harvard | Asignaturas de la malla |
|---|---|
| [CS50x](https://cs50.harvard.edu/x/) | Fundamentos Computacionales, Estructuras de Datos, Análisis de Algoritmos, Fundamentos de IA |
| [CS50 Python](https://cs50.harvard.edu/python/) | Introducción a la Programación, POO, Programación Avanzada |
| [CS50 SQL](https://cs50.harvard.edu/sql/) | Fundamentos de Base de Datos, Base de Datos Avanzada |
| [CS50 Web](https://cs50.harvard.edu/web/) | Ingeniería Web, Programación Avanzada |
| [CS50 Cybersecurity](https://cs50.harvard.edu/cybersecurity/) | Seguridad de la Información |
| [CS50 AI](https://cs50.harvard.edu/ai/) | Fundamentos de IA, Representación del Conocimiento, Sistemas Inteligentes, Estructuras de Datos |
| [CS50 R](https://cs50.harvard.edu/r/) | Fundamentos de Análisis de Datos |
| [CS50 Games](https://cs50.harvard.edu/games/) | Plataformas para Juegos |

Los títulos de los temas y los subtemas están redactados para el prototipo a partir de esos temarios; el contenido de las clases pertenece a Harvard.

## Herramientas de IA utilizadas

- **Claude Code (Anthropic):** estructuración de los datos, programación del índice de recuperación y de la interfaz, y pruebas de cada función.
- **Google AI Studio (Gemini):** prueba del tutor RAG sin programación (ver `prompts/`).
