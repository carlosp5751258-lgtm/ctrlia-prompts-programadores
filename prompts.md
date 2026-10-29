# 30 prompts para programadores (versión gratis)

_Prompts originales en español para depurar, refactorizar, probar, documentar, diseñar y crecer profesionalmente con asistentes de IA._

## Cómo usar estos prompts

1. Copia el prompt y reemplaza cada marcador entre corchetes (`[LENGUAJE]`, `[CÓDIGO]`, etc.) con tu información real.
2. Cuanto más contexto concreto pegues (código, errores, versiones), mejor será la respuesta.
3. Si el asistente se equivoca o inventa, pídele que razone paso a paso y que diga explícitamente cuando no esté seguro.
4. Revisa siempre el código generado antes de usarlo: tú sigues siendo responsable de lo que llega a producción.
5. No pegues secretos (contraseñas, tokens, claves privadas) ni datos personales de clientes en ningún asistente.

## 1. Debugging

### 1. Diagnóstico a partir de un stack trace

**Cuándo usarlo:** Cuando tienes un error con traza y no sabes por dónde empezar.

```text
Actúa como desarrollador senior de [LENGUAJE]. Te paso un error y su stack trace:
[ERROR_Y_STACK_TRACE]
Y el código relevante:
[CÓDIGO]
Explica en orden: 1) qué significa el error, 2) la línea exacta donde se origina y por qué, 3) las 3 causas más probables ordenadas por probabilidad, 4) cómo confirmar cada una con un experimento mínimo. No propongas el arreglo hasta haber razonado la causa.
```

### 2. Bug que solo ocurre a veces

**Cuándo usarlo:** Cuando un fallo aparece y desaparece sin patrón claro.

```text
Tengo un bug intermitente en [LENGUAJE]/[FRAMEWORK]: [DESCRIPCIÓN_DEL_SÍNTOMA]. Ocurre aproximadamente [FRECUENCIA] y no logro reproducirlo de forma fiable. Código involucrado:
[CÓDIGO]
Lista las fuentes típicas de no-determinismo que aplican aquí (concurrencia, orden de iteración, tiempo, caché, red, estado compartido) y para cada una dime qué log o assert agregar para atraparla.
```

### 3. Depuración por bisección

**Cuándo usarlo:** Cuando sabes que algo se rompió entre dos versiones.

```text
Este comportamiento funcionaba en la versión [VERSIÓN_BUENA] y falla en [VERSIÓN_MALA]. Explícame paso a paso cómo usar `git bisect` para encontrar el commit culpable, incluyendo cómo automatizarlo con `git bisect run` y un script de prueba para este caso: [CÓMO_SE_MANIFIESTA_EL_FALLO]. Escribe ese script en [LENGUAJE_O_BASH].
```


## 2. Refactorización

### 11. Refactor seguro en pasos pequeños

**Cuándo usarlo:** Cuando necesitas mejorar código existente sin romper nada.

```text
Quiero refactorizar este código en [LENGUAJE] sin cambiar su comportamiento:
[CÓDIGO]
Propón una secuencia de pasos pequeños, cada uno compilable y verificable por separado, indicando qué prueba ejecutar tras cada paso. Muestra el código final y explica qué mejoró en legibilidad y mantenibilidad.
```

### 12. Dividir una función gigante

**Cuándo usarlo:** Cuando una función es tan larga que da miedo tocarla.

```text
Esta función de [NÚMERO] líneas hace demasiadas cosas:
[CÓDIGO]
Identifica sus responsabilidades, propone nombres de funciones más pequeñas con su firma y sus entradas/salidas, y reescribe el código aplicando 'extraer función'. Mantén la misma interfaz pública.
```

### 13. Eliminar duplicación

**Cuándo usarlo:** Cuando dudas si aplicar DRY o si estarías creando una abstracción prematura.

```text
Estos fragmentos de [LENGUAJE] se parecen mucho:
[FRAGMENTO_1]
[FRAGMENTO_2]
¿Es duplicación real o solo coincidencia (dos cosas que cambiarán por motivos distintos)? Si conviene unificarlos, propón la abstracción mínima; si no, explica por qué es mejor dejarlos separados.
```


## 3. Tests

### 21. Pruebas unitarias completas

**Cuándo usarlo:** Cuando tienes una función nueva y quieres cubrirla bien desde el principio.

```text
Escribe pruebas unitarias en [FRAMEWORK_DE_TESTS] para esta función de [LENGUAJE]:
[CÓDIGO]
Cubre: caso feliz, valores límite, entradas inválidas, nulos/vacíos y errores esperados. Usa nombres de prueba descriptivos en formato 'debería_..._cuando_...' y el patrón Arrange-Act-Assert.
```

### 22. Casos borde que olvidé

**Cuándo usarlo:** Cuando tus tests pasan pero no confías del todo en ellos.

```text
Estas son mis pruebas actuales para [FUNCIÓN]:
[TESTS]
Y la implementación:
[CÓDIGO]
Lista los casos borde que NO estoy probando (límites numéricos, Unicode, zonas horarias, concurrencia, colecciones vacías o enormes, etc.) y escribe las pruebas que faltan.
```

### 23. Mocks y dobles de prueba

**Cuándo usarlo:** Cuando una prueba depende de servicios externos, reloj o red.

```text
Necesito probar esta clase en [LENGUAJE] que depende de [DEPENDENCIA_EXTERNA]:
[CÓDIGO]
Muestra cómo aislarla usando [LIBRERÍA_DE_MOCKS]. Explica cuándo usar stub, mock o fake en este caso y evita mockear lo que no es tuyo cuando haya una alternativa mejor.
```


## 4. Code review

### 31. Revisión completa de un PR

**Cuándo usarlo:** Antes de aprobar o enviar un pull request.

```text
Actúa como revisor senior. Revisa este diff en [LENGUAJE]:
[DIFF]
Contexto del cambio: [OBJETIVO_DEL_PR]. Clasifica tus comentarios en: bloqueante, importante y sugerencia. Para cada uno indica archivo/línea, el problema y una propuesta concreta. Termina con un resumen de 3 líneas.
```

### 32. Revisión de seguridad

**Cuándo usarlo:** Cuando el código maneja entrada de usuarios, datos sensibles o permisos.

```text
Revisa este código de [TIPO_DE_COMPONENTE] en [LENGUAJE] buscando vulnerabilidades:
[CÓDIGO]
Enfócate en inyección (SQL, comandos), XSS, autenticación/autorización, manejo de secretos, deserialización insegura y validación de entrada. Para cada hallazgo: severidad, escenario de explotación y corrección.
```

### 33. Revisión de concurrencia

**Cuándo usarlo:** Cuando hay hilos, async, workers o colas involucrados.

```text
Este código en [LENGUAJE] se ejecuta desde varios hilos/tareas a la vez:
[CÓDIGO]
Busca condiciones de carrera, interbloqueos, accesos no sincronizados a estado compartido y operaciones no atómicas. Describe un intercalado concreto de ejecución que provoque cada problema.
```


## 5. Documentación

### 41. README de proyecto

**Cuándo usarlo:** Cuando empiezas o publicas un proyecto.

```text
Escribe un README.md para este proyecto: [DESCRIPCIÓN]. Stack: [STACK]. Incluye: descripción en una frase, captura o ejemplo de uso, requisitos, instalación paso a paso, configuración (variables de entorno), cómo ejecutar pruebas, estructura del proyecto y cómo contribuir. Usa un tono directo y comandos copiables.
```

### 42. Docstrings y comentarios útiles

**Cuándo usarlo:** Cuando el código carece de documentación o tiene comentarios inútiles.

```text
Agrega documentación a este código en [LENGUAJE] siguiendo el estilo [ESTILO, ej. JSDoc, Google docstrings]:
[CÓDIGO]
Documenta el 'por qué' y los contratos (parámetros, retorno, excepciones, efectos secundarios), no repitas lo que el código ya dice. Elimina comentarios obsoletos o redundantes.
```

### 43. Documentar una API REST

**Cuándo usarlo:** Cuando necesitas documentar o formalizar una API existente.

```text
Genera documentación en formato OpenAPI 3 (YAML) para estos endpoints:
[CÓDIGO_DE_RUTAS_O_DESCRIPCIÓN]
Incluye esquemas de petición y respuesta, códigos de error, ejemplos realistas y descripción de autenticación.
```


## 6. Arquitectura y diseño

### 51. Diseño de un sistema desde cero

**Cuándo usarlo:** Al iniciar un proyecto nuevo o una funcionalidad grande.

```text
Necesito diseñar [SISTEMA] con estos requisitos: [REQUISITOS_FUNCIONALES]. Restricciones: [USUARIOS_ESPERADOS], [PRESUPUESTO], [EQUIPO]. Propón una arquitectura inicial simple, sus componentes, flujo de datos, almacenamiento y los puntos que habría que cambiar si crece 10 veces. Justifica por qué no elegiste opciones más complejas.
```

### 52. Comparar alternativas técnicas

**Cuándo usarlo:** Cuando debes elegir una base de datos, framework o servicio.

```text
Estoy decidiendo entre [OPCIÓN_A], [OPCIÓN_B] y [OPCIÓN_C] para [CASO_DE_USO]. Mi contexto: [EQUIPO, EXPERIENCIA, ESCALA, PLAZOS]. Haz una tabla comparativa con criterios relevantes para MI contexto, señala qué información me falta para decidir y da una recomendación con sus condiciones.
```

### 53. Modelado de dominio

**Cuándo usarlo:** Cuando empiezas a modelar un negocio en código.

```text
Este es el dominio de mi aplicación: [DESCRIPCIÓN_DEL_NEGOCIO]. Identifica entidades, objetos de valor, agregados y sus relaciones. Señala invariantes de negocio que el modelo debe proteger y propón las clases o tipos en [LENGUAJE].
```


## 7. SQL y bases de datos

### 61. Escribir una consulta compleja

**Cuándo usarlo:** Cuando necesitas una consulta que no sabes armar.

```text
Tengo estas tablas en [MOTOR_SQL]:
[ESQUEMA]
Necesito obtener: [RESULTADO_DESEADO]. Escribe la consulta, explica cada parte (JOINs, agrupaciones, subconsultas o CTEs) y muestra un pequeño ejemplo de datos con el resultado esperado.
```

### 62. Optimizar una consulta lenta

**Cuándo usarlo:** Cuando una consulta es el cuello de botella de tu aplicación.

```text
Esta consulta en [MOTOR_SQL] tarda [TIEMPO] sobre una tabla de [N_FILAS] filas:
[CONSULTA]
Plan de ejecución:
[EXPLAIN_ANALYZE]
Interpreta el plan, señala la operación más costosa y propón índices o reescrituras. Indica el costo de cada índice en escrituras.
```

### 63. Diseño de esquema

**Cuándo usarlo:** Al comenzar un proyecto con base de datos relacional.

```text
Diseña el esquema relacional en [MOTOR_SQL] para [DOMINIO]. Requisitos: [REQUISITOS]. Incluye tablas, tipos de columnas, claves primarias y foráneas, restricciones (NOT NULL, UNIQUE, CHECK) e índices iniciales. Justifica dónde normalizas y dónde no.
```


## 8. DevOps y CI/CD

### 71. Dockerfile optimizado

**Cuándo usarlo:** Cuando vas a contenerizar una aplicación.

```text
Escribe un Dockerfile para una aplicación [LENGUAJE]/[FRAMEWORK] que se ejecuta con [COMANDO]. Usa build multi-etapa, imagen base mínima, usuario no root, aprovechamiento de caché de capas y .dockerignore. Explica cada decisión y el tamaño aproximado esperado.
```

### 72. Pipeline de CI

**Cuándo usarlo:** Cuando quieres automatizar pruebas y despliegues.

```text
Crea un workflow de [GITHUB_ACTIONS_O_GITLAB_CI] para un proyecto [LENGUAJE] que: instale dependencias con caché, ejecute linter, pruebas y build, y solo despliegue en la rama [RAMA]. Usa versiones fijas de las acciones y secretos del sistema de CI, nunca credenciales en el archivo.
```

### 73. Docker Compose para desarrollo local

**Cuándo usarlo:** Cuando quieres que todo el equipo levante el entorno con un comando.

```text
Escribe un docker-compose.yml para desarrollo local con: [SERVICIOS, ej. app, PostgreSQL, Redis]. Incluye volúmenes para persistencia, healthchecks, variables de entorno desde un archivo .env y recarga en caliente del código. Explica cómo levantarlo y resetear los datos.
```


## 9. Aprendizaje

### 81. Aprender un lenguaje nuevo viniendo de otro

**Cuándo usarlo:** Cuando cambias de stack o empiezas un lenguaje nuevo.

```text
Sé programar bien en [LENGUAJE_QUE_DOMINO] y quiero aprender [LENGUAJE_NUEVO]. Explícame las diferencias más importantes en: tipos, manejo de errores, concurrencia, gestión de memoria y herramientas. Para cada una muestra el mismo ejemplo en ambos lenguajes y las trampas típicas para alguien con mi experiencia.
```

### 82. Explicar un concepto con niveles

**Cuándo usarlo:** Cuando un concepto no termina de hacerte clic.

```text
Explícame [CONCEPTO] en tres niveles: 1) en una frase para alguien sin experiencia, 2) con una analogía y un ejemplo de código en [LENGUAJE], 3) los detalles avanzados y los errores comunes. Termina con 3 preguntas para verificar que entendí.
```

### 83. Plan de estudio personalizado

**Cuándo usarlo:** Cuando quieres aprender algo de forma estructurada.

```text
Quiero aprender [TEMA] en [SEMANAS] semanas dedicando [HORAS] horas por semana. Mi nivel actual: [NIVEL]. Crea un plan semanal con objetivos concretos, recursos de tipo genérico (documentación oficial, libros clásicos), un mini proyecto por semana y cómo saber si estoy listo para avanzar.
```


## 10. Productividad y carrera

### 91. Dividir una tarea grande

**Cuándo usarlo:** Cuando una tarea parece demasiado grande para empezar.

```text
Tengo que implementar [FUNCIONALIDAD] en [PROYECTO]. Divídela en tareas de máximo medio día cada una, ordenadas por dependencias, con criterio de 'terminado' para cada una e identifica cuáles se pueden entregar de forma independiente para obtener feedback temprano.
```

### 92. Estimación con incertidumbre

**Cuándo usarlo:** Cuando te piden una estimación y no quieres comprometerte a ciegas.

```text
Necesito estimar [TAREA]. Contexto: [CONTEXTO_TÉCNICO]. Dame una estimación en rango (optimista, probable, pesimista), lista las incógnitas que más afectan el rango y qué spike o investigación de pocas horas reduciría la incertidumbre.
```

### 93. Mensajes de commit claros

**Cuándo usarlo:** Cada vez que vas a hacer commit de algo no trivial.

```text
Escribe un mensaje de commit siguiendo Conventional Commits para este diff:
[DIFF]
Usa un título de máximo 72 caracteres en imperativo y un cuerpo que explique el por qué del cambio, no el cómo. Si el diff mezcla cambios no relacionados, sugiere cómo dividirlo en varios commits.
```

