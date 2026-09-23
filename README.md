# Colab_VotaConCiencia

# VotaConCiencia: Sistema de Autogestión y Viabilidad de Propuestas con IA

## Quiero llamar su atención para que revise otro proyecto que he desarrollado para lo mismo, está hecho en Python con VSC.
## Quiero que me de su opinión al respecto. 

## https://github.com/Oorozcoh/Secre

## Resumen
VotaConCiencia es una plataforma tecnológica orientada a optimizar la gestión, recolección y análisis preliminar de propuestas estudiantiles en el entorno escolar. Utilizando un enfoque Full Stack combinado con inteligencia artificial generativa, el sistema permite a los candidatos postular sus iniciativas, autenticarse de forma segura mediante un portal dedicado y someter sus ideas a un análisis automatizado de viabilidad operativa mediante modelos de lenguaje avanzados. Este proyecto se presenta como una Prueba de Concepto (PoC) integral que une el desarrollo web con técnicas avanzadas de *fast prompting*.

---

## Introducción

### Nombre del Proyecto
**VotaConCiencia: Autogestión de Propuestas y Módulo de Viabilidad por Inteligencia Artificial**

### Presentación del Problema
En los procesos de participación y gobierno escolar (como las elecciones de representantes estudiantiles), los participantes presentan múltiples propuestas de mejora institucional. No obstante, los comités evaluadores se enfrentan a una saturación de información y a la dificultad técnica para filtrar qué iniciativas son viables, realistas en tiempos de ejecución y ajustadas a los presupuestos o recursos reales de la institución. Esto genera retrasos en la retroalimentación y limita el impacto pedagógico del ejercicio democrático.

### Desarrollo de la Propuesta de Solución
Para resolver esta problemática, la arquitectura integra dos modelos de IA:
1. **Modelo Texto-Texto (Análisis de Viabilidad):** A través de la API de OpenAI (`gpt-4o-mini`), se procesan las propuestas de los estudiantes aplicando técnicas de ingeniería de prompts (roles estructurados, delimitadores y formato estricto) para evaluar su factibilidad, calcular riesgos y emitir un puntaje cuantitativo y cualitativo.
2. **Modelo Texto-Imagen:** Se emplean prompts optimizados para la generación visual de material de campaña y pósteres informativos que apoyen la difusión de las propuestas aprobadas.

### Justificación de la Viabilidad del Proyecto
El proyecto es altamente viable desde el punto de vista técnico, temporal y financiero. Está construido utilizando tecnologías estándar de bajo costo y alta eficiencia (Python, Django, SQLite, Streamlit y JavaScript). El uso de modelos optimizados como `gpt-4o-mini` minimiza drásticamente los costos operativos y los tiempos de inferencia, haciéndolo totalmente sostenible para implementaciones en instituciones educativas de escala moderada.

---

## Objetivos

### Objetivo General
Desarrollar una Prueba de Concepto (PoC) funcional y un sistema web integrado que automatice la evaluación de viabilidad de propuestas estudiantiles mediante el uso de modelos de lenguaje e inteligencia artificial generativa.

### Objetivos Específicos
* Implementar un flujo de autenticación seguro para candidatos validado mediante una base de datos relacional.
* Diseñar e implementar prompts estructurados (*fast prompting*) optimizados para el análisis de viabilidad escolar.
* Incorporar medición analítica de consumo de tokens y estimación de costos por llamada a la API para justificar la eficiencia del flujo.
* Comparar metodologías de prompting (*zero-shot* vs. *few-shot*) para maximizar la precisión de las respuestas del modelo.
* Documentar y generar recursos visuales de apoyo mediante prompts de texto-imagen con herramientas de IA externas.

---

## Metodología
El desarrollo del proyecto se estructuró en las siguientes fases metodológicas:
1. **Levantamiento y Modelado de Datos:** Definición de entidades (`Candidato`, atributos de propuestas y campos de viabilidad) en Django.
2. **Diseño de Interfaz y Endpoints de API:** Creación del panel de autogestión y las rutas asíncronas para la sincronización de datos con el frontend.
3. **Experimentación y Refinamiento (PoC en Jupyter Notebook):** Pruebas iterativas comparando enfoques de prompting y aplicando manejo robusto de excepciones (`try/except`).
4. **Validación con Casos Reales:** Pruebas funcionales procesando propuestas estudiantiles reales del entorno escolar.

---

## Herramientas y Tecnologías
* **Backend:** Python, Django, SQLite.
* **Frontend:** HTML5, CSS3 (interfaz moderna en modo oscuro con acentos cian), JavaScript (Fetch API).
* **Inteligencia Artificial:** OpenAI API (`gpt-4o-mini`), librerías de gestión de tokens y control de excepciones.
* **Entorno de Experimentación:** Jupyter Notebook / Google Colab con gestión segura de credenciales (`userdata`).
* **Control de Versiones:** Git y GitHub.

---

## Implementación y PoC (Jupyter Notebook)
La lógica de experimentación, llamadas al modelo y análisis métrico se encuentra documentada en el archivo `VotaConCiencia.ipynb`. A continuación se destacan los componentes clave implementados:

### 1. Invocación de la API con Manejo de Errores y Métricas de Tokens
Se configuró el cliente oficial de OpenAI implementando bloques `try/except` robustos y extracción de metadatos de consumo para calcular la eficiencia financiera:

```python
try:
    response = client.chat.completions.create(
        model="gpt-4o-mini",
        messages=[{"role": "system", "content": system_prompt}, {"role": "user", "content": user_prompt}],
        temperature=0.7
    )

    # Extracción de métricas de uso y costos estimados
    usage = response.usage
    total_tokens = usage.total_tokens
except OpenAIError as e:
    print(f"Error en la API: {e}")
```

### 2. Experimentación de Prompts (Zero-shot vs. Few-shot)

    Zero-shot: Se le indica al modelo directamente el rol y la tarea sin ejemplos previos.

    Few-shot: Se incorporan casos de estudio y ejemplos resueltos de viabilidad previa en el system prompt para alinear la estructura del resultado JSON devuelto, reduciendo al mínimo los errores de formato.

### 3. Pruebas con Propuestas Estudiantiles Reales

La libreta ejecuta simulaciones basadas en casos verídicos del entorno escolar (por ejemplo, iniciativas de reciclaje automatizado y torneos tecnológicos propuestos por estudiantes de distintos ciclos), validando la coherencia del análisis de viabilidad.
### 4. Generación Visual (Texto a Imagen)

    Estrategia aplicada: Siguiendo las directrices técnicas del proyecto para entornos de producción y costos, los prompts visuales fueron optimizados y ejecutados en herramientas de IA externas especializadas.

    Prompt Utilizado: "Un póster estudiantil futurista y limpio, estilo corporativo moderno y tecnológico, con acentos en tonos cian y oscuros, que promueva la innovación y la participación democrática en un colegio."

    Evidencia: La imagen resultante se encuentra almacenada en el directorio /assets/ de este repositorio para su inspección directa.

## Resultados

    Precisión y Estructura: La aplicación de fast prompting con técnicas de delimitación permitió estandarizar las respuestas del modelo, facilitando su almacenamiento automatizado en la base de datos para que los candidatos consulten su retroalimentación en tiempo real.

    Eficiencia Financiera: Mediante el monitoreo estricto de tokens (prompt_tokens y completion_tokens), se comprobó que el costo operativo por cada análisis con gpt-4o-mini representa fracciones mínimas de centavo de dólar, garantizando la viabilidad económica a gran escala.

### Conclusiones

El desarrollo del proyecto VotaConCiencia demuestra que la integración de la inteligencia artificial generativa en procesos de gestión escolar es completamente viable y transformadora. La unión de una interfaz web funcional con una PoC robusta en Jupyter Notebook permitió superar los retos de integración asíncrona, cumplir con rigurosos estándares de manejo de errores y optimizar los recursos institucionales mediante el uso eficiente de modelos de lenguaje.


### Referencias

    Documentación Oficial de Django: https://docs.djangoproject.com/

    OpenAI API Documentation & Best Practices: https://platform.openai.com/docs/

    Guías de Ingeniería de Prompts y Optimización de Costos de OpenAI.
