# Biblioteca de prompts — Laboratorio 06 
## Prueba 1 — [ Prompt vago vs. prompt estructurado] 
**Herramienta:** Claude 

**Prompt Vago:** 
Escribe un correo pidiendo más plazo para un trabajo.

**Resultado:** el correo salió genérico y con muchos campos por completar entre corchetes (docente, curso, trabajo, fechas y motivo). Como no había datos, tuve que inventar una estructura general.

**Prompt Estructurado:** 

 =Rol 
Actúa como un estudiante universitario que se comunica de forma formal y respetuosa. 

= Contexto 
Debo entregar el informe del proyecto final del curso de Diseño de Interfaces el  viernes, 
pero dos integrantes del equipo estuvieron enfermos esta semana. 

= Tarea 
Redacta un correo al docente solicitando una prórroga de 3 días. 

= Formato de salida 
Incluye asunto, saludo, cuerpo en máximo 2 párrafos y despedida. 

= Restricciones 
No exageres la situación, no uses más de 120 palabras y propone una nueva fecha  concreta.

**Resultado:** tenía rol, contexto, tarea, formato de salida y restricciones. El correo salió específico, con el curso, el motivo (integrantes enfermos) y una nueva fecha concreta, y respetó el límite de 120 palabras y los dos párrafos.

**Observaciones:** Cuanto más contexto y restricciones se dan, menos hay que corregir después. El prompt vago obliga a completar datos a mano y el estructurado da un resultado casi listo para enviar.

# Biblioteca de prompts — Laboratorio 06
## Prueba 2 — [ Zero-shot y few-shot ]
**Herramienta:** Claude

**Prompt Zero-shot:**
Clasifica cada comentario como POSITIVO, NEGATIVO o NEUTRO.

1. "La app se cierra cada vez que intento pagar."
2. "Llegó el pedido, nada que destacar."
3. "Me encantó lo rápido que cargan las pantallas."
4. "Está bien, aunque el botón de ayuda es difícil de encontrar."

**Resultado:** clasificó los cuatro comentarios con las tres categorías disponibles, con un formato libre y sin indicar el tema. El comentario 4 quedó como NEUTRO o POSITIVO porque no existía la categoría MIXTO.

**Prompt Few-shot:**
Clasifica cada comentario siguiendo el formato de los ejemplos.

Comentario: "Excelente diseño, todo es muy intuitivo."
Categoría: POSITIVO | Tema: diseño

Comentario: "Buen precio, pero la entrega tardó una semana."
Categoría: MIXTO | Tema: entrega

Comentario: "La app se cierra cada vez que intento pagar."
Categoría:

Comentario: "Está bien, aunque el botón de ayuda es difícil de encontrar."
Categoría:

**Resultado:** respondió con el formato "Categoría | Tema": el comentario del pago como NEGATIVO (tema: estabilidad de la app) y el del botón de ayuda como MIXTO (tema: ayuda o usabilidad).

**Observaciones:** con los ejemplos, la respuesta respetó el formato, identificó el tema y usó la categoría MIXTO, que solo se entiende a partir de los ejemplos. Sin ejemplos, el modelo no conocía ni el formato ni ese criterio.


# Biblioteca de prompts — Laboratorio 06
## Prueba 3 — [ Delimitadores y formato de salida ]
**Herramienta:** Claude

**Prompt Resumen con delimitadores:**
Resume el texto delimitado por <texto></texto> en 3 viñetas de máximo 20 palabras cada una.
Luego escribe una sola oración con la idea principal.

<text >
(pegar aquí el texto de al menos 200 palabras)
 < /texto>

**Resultado:** devolvió 3 viñetas de máximo 20 palabras y una sola oración final con la idea principal, sin mezclar las instrucciones con el contenido del texto.

**Prompt Extracción estructurada:**
Del siguiente mensaje extrae: nombre, curso, fecha y motivo.
Devuelve primero una tabla Markdown y después el mismo contenido en JSON válido. Si algún dato no aparece, escribe "no especificado".

"""

Hola, soy Lucía Ramos del curso de Base de Datos. Quería avisar que el martes 14 no podré asistir al laboratorio porque tengo una cita médica.

"""


**Resultado:** entregó una tabla Markdown (columnas Campo y Valor) con nombre (Lucía Ramos), curso (Base de Datos), fecha (martes 14) y motivo (cita médica), seguida del mismo contenido en un bloque JSON válido. Además, indicó que el mensaje no trae mes ni año y dejó la fecha tal como aparece.

**Observaciones:** El asistente también señaló por su cuenta un dato incompleto (mes y año), lo que muestra que la instrucción "no especificado" se interpretó con criterio y no solo de forma literal.


# Biblioteca de prompts — Laboratorio 06
## Prueba 4 — [ Razonamiento paso a paso y encadenamiento ]
**Herramienta:** Claude

**Prompt Razonamiento paso a paso:**
Tengo 3 tareas para esta semana:
- Informe de laboratorio (4 h, entrega miércoles)
- Estudiar para el examen (6 h, examen viernes)
- Presentación grupal (3 h, jueves)
Dispongo de 3 horas libres por día de lunes a jueves.

Piensa paso a paso: primero calcula las horas disponibles, luego verifica si alcanzan y finalmente propone un horario día por día en una tabla.

**Resultado:** mostró primero el cálculo (3 h × 4 días = 12 h disponibles frente a 13 h requeridas), detectó que faltaba 1 hora y luego presentó una tabla día por día con las tareas repartidas según sus fechas límite.

**Prompt Encadenamiento:**
# Prompt 1
Genera el índice (máximo 5 secciones) de un artículo de blog titulado "Buenas prácticas para diseñar APIs REST".
# Prompt 2
Desarrolla solo la sección 2 del índice anterior en 150 palabras, con un ejemplo de endpoint.
# Prompt 3
Revisa la sección que escribiste y sugiere 3 mejoras de claridad.

**Resultado:**
- Prompt 1: generó un índice de 5 secciones, desde "Por qué importa el diseño de una API" hasta "Seguridad y documentación".
- Prompt 2: desarrolló solo la sección 2 ("Nombrar recursos y usar bien los verbos HTTP") en unas 150 palabras, con un ejemplo de endpoints (GET /usuarios/25, POST /usuarios y DELETE /usuarios/25) y un ejemplo de recurso anidado (GET /usuarios/25/pedidos).
- Prompt 3: sugirió 3 mejoras de claridad sobre el texto que había escrito: separar las ideas del primer párrafo, marcar el contraste entre lo correcto y lo incorrecto, y reemplazar expresiones vagas por reglas concretas. Además, ofreció reescribir la sección aplicando esas mejoras.

**Observaciones:** el encadenamiento funcionó porque cada prompt usó la salida del anterior sin repetir el contexto: el asistente identificó la sección 2 a partir del índice y revisó "la sección que escribiste" con referencias concretas a su propio texto (por ejemplo, señaló expresiones vagas como "con moderación"). Dividir la tarea en etapas permitió controlar el resultado en cada paso y corregir antes de avanzar. Pedir el razonamiento antes de la respuesta final, en el Paso 4.1, permitió detectar que las horas no alcanzaban, algo que una respuesta directa podría haber pasado por alto.


## Rúbrica de evaluación

| Criterio    | Descripción                                   | Puntaje(1-5) |
| ----------- | --------------------------------------------- | :-----------: |
| Relevancia  | Responde exactamente lo que se pidió          |  4             |
| Precisión   | La información es correcta y sin inventos     |        5       |
| Formato     | Respeta la estructura y extensión solicitadas |        5       |
| Tono        | Es adecuado para el público objetivo          |       5        |



## Iteraciones — Plan de estudio para un examen

**Herramienta:** Claude

**Prompt v1:**
Hazme un plan de estudio para un examen.

**Resultado v1:** entregó un plan genérico y largo, sin fechas ni temas concretos, porque el prompt no indicaba la materia ni el tiempo disponible.

**Prompt v2:**
Actúa como un tutor universitario. Soy estudiante de software y tengo un examen de JavaScript en una semana. Hazme un plan de estudio.

**Resultado v2:** el plan se adaptó a JavaScript y a una semana de preparación, con un tono de tutor. Sin embargo, el formato fue libre y la respuesta salió extensa.

**Prompt v3:**
Actúa como un tutor universitario. Soy estudiante de software y tengo un examen de JavaScript en una semana. Hazme un plan de estudio. Preséntalo en una tabla día por día, con máximo 2 horas diarias y en menos de 150 palabras.

**Resultado v3:** entregó una tabla día por día con un máximo de 2 horas diarias, dentro del límite de palabras y lista para usar sin ediciones.

### Evaluación con la rúbrica

| Criterio   | v1 | v2 | v3 |
| ---------- | :-: | :-: | :-: |
| Relevancia |  3  |  4  |  5  |
| Precisión  |  3  |  4  |  4  |
| Formato    |  2  |  3  |  5  |
| Tono       |  3  |  4  |  5  |
| **Total**  | **11** | **15** | **19** |

### Resumen de iteraciones

| Versión | Cambio realizado en el prompt                                       | Puntaje total |
| ------- | ------------------------------------------------------------------- | :-----------: |
| v1      | Prompt inicial sin estructura                                       |     11/20     |
| v2      | Se agregó rol (tutor universitario) y contexto (JavaScript, 1 semana) |     15/20     |
| v3      | Se definió formato (tabla día por día) y restricciones (2 h diarias, menos de 150 palabras) |     19/20     |

**Observaciones:** en v2, el rol y el contexto mejoraron la relevancia, la precisión y el tono, porque la respuesta dejó de ser genérica y se ajustó al examen y al tiempo real. En v3, el formato y las restricciones fueron lo que más subió el puntaje, ya que la respuesta quedó breve, ordenada y lista para usar. Cada iteración agregó un tipo de información distinto: primero quién responde y para qué situación, luego cómo debe entregarse.


# Plantillas reutilizables

## Plantilla: Redacción de correo formal
**Variables:** rol, situación, destinatario, objetivo, n, palabras, tono

```text
Actúa como {{rol}}.
Contexto: {{situación}}.
Redacta un correo dirigido a {{destinatario}} para {{objetivo}}.
Formato: asunto, saludo, cuerpo en máximo {{n}} párrafos y despedida.
Restricciones: máximo {{palabras}} palabras, tono {{tono}}.
```

**Ejemplo de uso:** rol = un estudiante universitario, situación = el informe final del curso de Diseño de Interfaces vence el viernes y dos integrantes del equipo estuvieron enfermos, destinatario = el docente, objetivo = solicitar una prórroga de 3 días, n = 2, palabras = 120, tono = formal y respetuoso.


## Plantilla: Resumen con delimitadores
**Variables:** n, palabras, texto

```text
Resume el texto delimitado por <texto></texto> en {{n}} viñetas de máximo {{palabras}} palabras cada una.
Luego escribe una sola oración con la idea principal.

<texto>
{{texto}}
</texto>
```

**Ejemplo de uso:** n = 3, palabras = 20, texto = una noticia o un fragmento del material del curso.


