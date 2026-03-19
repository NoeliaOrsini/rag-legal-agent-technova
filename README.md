# Agente IA con RAG – TechNova Solutions S.A.

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/NoeliaOrsini/rag-legal-agent-technova/blob/main/Inmersion_agentes_IA_clase_2y3_Asistente_Legal.ipynb)

Este proyecto fue desarrollado en el marco de la Inmersión IA Dev de Alura Latam, a lo largo de tres clases donde se construyó, paso a paso, un agente capaz de responder consultas combinando información interna y externa.

El resultado es un asistente legal que trabaja sobre una empresa ficticia, TechNova Solutions S.A., utilizando datos estructurados de empleados, desempeño y vacaciones.

---

## Objetivo del proyecto

Construir un agente que no solo responda preguntas, sino que pueda:

- Consultar información interna (documentos)
- Evitar alucinaciones
- Decidir cuándo usar datos propios o información externa
- Generar respuestas fundamentadas

---

## Entorno de ejecución

Este proyecto fue desarrollado en Google Colab.

### 1. Cómo comenzar

Podés usar el proyecto de dos formas:

- Abrir el notebook directamente desde el botón **Open in Colab**  
- O clonar el repositorio:
git clone https://github.com/NoeliaOrsini/rag-legal-agent-technova.git

Si abrís en Colab, se recomienda hacer una copia:
Archivo → Guardar una copia en Drive

### 2. API Keys necesarias

Para ejecutar el notebook se deben configurar dos claves:

**GEMINI_API_KEY (Google Generative AI)**  
- Crear desde Google AI Studio  
- En Colab → "Secrets" (ícono 🔑) → agregar:
  copiá y pegá la api key y nombrala: GEMINI_API_KEY


**SERPAPI_API_KEY (búsquedas web)**  
- Crear cuenta en https://serpapi.com/  
- En Colab → "Secrets" → agregar:
  copiá y pegá la api key y nombrala: SERPAPI_API_KEY

### Ejecución del notebook

Una vez configuradas las API Keys:

- Ejecutar las celdas en orden desde el inicio  
- Al llegar a la sección de carga de PDFs, subir los archivos correspondientes  
- Luego continuar con la ejecución del resto de las celdas  

### Consideraciones

- El sistema puede arrojar errores si se alcanza el límite de uso (quota) de las APIs  
- En ese caso, será necesario esperar y continuar en otro momento o trabajar con menos datos (subconjuntos)

---

## Tecnologías utilizadas

- Python  
- Google Colab  
- Gemini (Google Generative AI)  
- LangChain  
- FAISS (vector store)  
- PyPDF  
- Tenacity  

---

## Evolución del proyecto

### Clase 1 – Construcción del agente

- Introducción a la lógica de agentes  
- Implementación inicial de RAG  
- Uso de datos ficticios de RRHH  
- Diseño con IDs anónimos para protección de datos  

---

### Clase 2 – Profundización en RAG (Python y Colab)

Se implementó el sistema completo en código:

- Carga de documentos PDF  
- División en fragmentos (chunking)  
- Generación de embeddings (transformación del texto en vectores numéricos)  
- Almacenamiento en FAISS para búsqueda por similitud  
- Recuperación de contexto relevante  

Ejemplo de búsqueda semántica:

    consulta = "¿cuántos empleados aún no tomaron vacaciones?"
    resultados = vectorstore1.similarity_search(consulta)

El sistema no busca coincidencias exactas, sino similitud de significado.

Configuración del modelo:

    llm = ChatGoogleGenerativeAI(
        model="gemini-2.5-flash",
        temperature=0.2
    )

Se utiliza una temperatura baja para lograr respuestas más objetivas y reducir alucinaciones.

---

### Clase 3 – Agente con toma de decisiones

Se incorporó lógica para que el agente determine cómo responder:

Flujo del sistema:

    Pregunta → Clasificación → (RAG | Web) → Contexto → LLM → Respuesta

- Usa RAG si la información está en los documentos  
- Usa Web si la consulta es general  

Esto permite combinar precisión en datos internos con cobertura en preguntas abiertas.

---

## Caso de uso

El agente funciona como un asistente legal interno, capaz de responder consultas sobre:

- Vacaciones del personal  
- Desempeño de empleados  
- Información estructurada de la empresa  

Trabaja sobre documentos ficticios de TechNova Solutions S.A., diseñados para simular un entorno real.

Los datos utilizados en este proyecto fueron inicialmente estructurados en una base tipo Excel y luego transformados en un documento PDF para su procesamiento dentro del sistema RAG.

Durante ese proceso, se reemplazaron nombres y apellidos por identificadores anónimos (IDs), incorporando desde el diseño criterios de protección de datos personales. Esto permite trabajar con información sensible en un entorno simulado, manteniendo una lógica alineada con buenas prácticas en materia de confidencialidad.

---

## Consideraciones técnicas

- El rendimiento depende de la calidad del chunking  
- El uso de embeddings puede estar limitado por cuotas de API  
- Se recomienda trabajar con subconjuntos de datos cuando hay múltiples documentos  
- Google Colab utiliza memoria temporal (requiere reejecución)  

---

## Seguridad

Las API Keys se gestionan mediante Google Colab Secrets (`userdata`), evitando su exposición en el código.

---

## Mejora adicional

Se incorporó la posibilidad de exportar respuestas en formato PDF, acercando el desarrollo a un caso de uso práctico.

---

## Conclusión

Este proyecto muestra la evolución desde un modelo que responde preguntas, hacia un sistema que recupera información relevante y finalmente un agente que decide cómo y desde dónde responder.

---

## Autor

Proyecto realizado por **Noelia Orsini**  
Abogada · Programadora · Counselor  

LinkedIn: [www.linkedin.com/in/noelia-orsini](https://www.linkedin.com/in/noelia-orsini)
