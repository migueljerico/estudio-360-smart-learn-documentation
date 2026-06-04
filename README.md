# Documentación del Proyecto Estudio 360 Smart Learn

## 📋 Descripción del Proyecto

Este repositorio documenta el proceso de creación de la miniaplicación web **Estudio 360 Smart Learn**, desarrollada utilizando la herramienta de IA Lovable. La aplicación está diseñada para el entorno educativo, facilitando la autoevaluación de alumnos de Educación Primaria y la gestión de contenido por parte del profesorado.

### Usuario Objetivo

Profesorado y alumnos de Educación Primaria.

### Problema que Resuelve

La aplicación aborda la necesidad de una autoevaluación estructurada y personalizada para alumnos, con una clara separación de roles que permite al profesorado gestionar y revisar el contenido de forma centralizada, mientras los alumnos acceden únicamente a su información y progreso individual.

## ✨ Funcionalidades Principales

### Para el Profesorado

*   Creación y edición de flashcards, quizzes y actividades por tema o unidad.
*   Asignación de contenido a clases o grupos específicos.
*   Visualización de resultados agregados por alumno y por pregunta.
*   Detección de preguntas con mayor tasa de fallo para reforzar la enseñanza.
*   Publicación de contenido nuevo y reutilización del ya creado.

### Para el Alumnado

*   Realización de autoevaluaciones cortas y repetibles.
*   Seguimiento de su progreso, aciertos, errores y temas pendientes.
*   Repaso de tarjetas falladas con mayor frecuencia.
*   Acceso exclusivo a su información y contenido asignado.
*   Recepción de feedback inmediato después de cada quiz.

## 🤖 Trabajo con Lovable (Prompts Utilizados)

La aplicación fue generada inicialmente utilizando el siguiente prompt en Lovable:

```
Crea una aplicación web educativa llamada Estudio 360 
La app debe tener dos roles principales: Profesor y Alumno.
Objetivo
La plataforma debe permitir que:
Los profesores creen, editen y asignen contenido educativo.
Los alumnos realicen autoevaluaciones personalizadas.
Cada alumno vea únicamente sus propios datos, progreso y resultados.
Los profesores puedan ver el contenido, resultados y progreso de sus alumnos.
Funcionalidades para Profesor
Crear, editar y eliminar flashcards.
Crear, editar y eliminar quizzes.
Organizar contenido por curso, tema y unidad.
Asignar contenido a uno o varios alumnos o grupos.
Ver el progreso de cada alumno.
Ver estadísticas globales de la clase.
Detectar preguntas con más fallos.
Crear nuevo contenido desde cero o duplicar contenido existente.
Funcionalidades para Alumno
Ver el contenido asignado por su profesor.
Estudiar flashcards en modo repaso.
Realizar quizzes de autoevaluación.
Ver resultados inmediatos al terminar.
Consultar su historial de intentos.
Ver métricas personales como aciertos, errores, progreso por tema y tiempo de estudio.
Repasar solo las tarjetas o preguntas que ha fallado.
Estructura de la aplicación
Página de inicio con acceso/login.
Panel de profesor.
Panel de alumno.
Biblioteca de contenidos.
Pantalla de creación de flashcards.
Pantalla de creación de quizzes.
Pantalla de estudio.
Pantalla de resultados y progreso.
Pantalla de administración de clases y alumnos.
Diseño
Interfaz moderna, limpia y minimalista.
Muy fácil de usar en móvil y escritorio.
Enfoque educativo profesional.
Colores agradables, con buena jerarquía visual.
Componentes claros, accesibles y bien organizados.
Modelo de datos
Incluye entidades para:
Usuarios
Roles
Clases
Alumnos
Profesores
Decks de flashcards
Quizzes
Preguntas
Respuestas
Intentos
Progreso por usuario
Asignaciones de contenido
Reglas importantes
Un alumno solo puede ver sus propios datos.
Un profesor puede ver el contenido y progreso de sus alumnos.
La experiencia debe estar centrada en el aprendizaje y la autoevaluación.
La app debe ser escalable para añadir repetición espaciada, gamificación e importación de contenido más adelante.
Resultado esperado
Genera la aplicación completa con estructura funcional, diseño atractivo y navegación clara entre los paneles de profesor y alumno.
```

## 🔄 Iteraciones y Mejoras

### Mejora 1

**Problema detectado:** La generación inicial de Lovable produjo las tarjetas y cuestionarios en inglés (`decks` y `quizzes`).

**Cambio realizado:** Se modificó el contenido a castellano para adaptarlo al público objetivo.

## 🚀 Despliegue

La aplicación ha sido desplegada y es accesible a través de los siguientes enlaces:

*   **Vercel:** [https://estudio-360-smart-learn-vercel.vercel.app/](https://estudio-360-smart-learn-vercel.vercel.app/)
*   **Netlify:** [https://estudio360.netlify.app/](https://estudio360.netlify.app/)

### Comentarios Técnicos sobre el Despliegue

El despliegue inicial en Vercel presentó un error 404. Tras una revisión y el despliegue exitoso en Netlify (donde el agente IA de Netlify corrigió el código automáticamente), se identificó que el problema en Vercel se debía a un cambio necesario en el código de `preset` de Vercel a Netlify. Una vez realizado este ajuste, la aplicación pudo ser desplegada correctamente en Vercel.

## 💡 Reflexión Final

### Facilidades y Dificultades

La parte más sencilla del proyecto fue la creación de la aplicación mediante Lovable, destacando la eficiencia de las herramientas de IA para la generación inicial. La mayor dificultad residió en el despliegue en Vercel, que resultó ser menos intuitivo para la depuración de errores en comparación con Netlify, cuyo agente IA facilitó la corrección automática.

### Riesgos y Limitaciones de Usar IA para Crear Aplicaciones

*   **Falta de control y mantenimiento:** La facilidad de implementar lógica sin una comprensión profunda puede dificultar la corrección de fallos o futuras actualizaciones.
*   **Errores y vulnerabilidades:** La IA puede generar soluciones incorrectas (alucinaciones), ignorar aspectos de seguridad o no manejar adecuadamente errores imprevistos.
*   **Visión limitada:** Aunque eficaz para tareas aisladas, la IA puede perder eficiencia en el diseño de arquitecturas complejas, globales o altamente escalables.

**Conclusión:** La IA es un excelente copiloto para acelerar el desarrollo, pero requiere supervisión humana constante para asegurar la calidad y robustez del producto final.

### Mejoras Futuras (Si se dispusiera de una semana adicional)

1.  **Generación de Cuestionarios Asistida por IA:** Integrar un flujo donde el profesor pueda introducir un tema o texto base, y la aplicación genere automáticamente un borrador de cuestionario (preguntas y respuestas de opción múltiple) para su validación. Esto reduciría la fricción inicial al poblar la plataforma.
2.  **Paneles de Análisis (Dashboards) Personalizados por Rol:** Desarrollar visualizaciones de datos específicas para profesores (métricas agregadas de clase, preguntas con mayor tasa de fallo) y alumnos (seguimiento personal de aciertos, errores, áreas de mejora y cuestionarios pendientes).
3.  **Automatización de Notificaciones y Feedback:** Implementar un sistema de avisos automáticos (correo electrónico o mensajería) para notificar a los profesores sobre nuevas asignaciones y a los alumnos sobre el feedback inmediato tras completar un quiz.

## 🛠️ Tecnologías Utilizadas

*   **Lovable:** Herramienta de IA para la generación de la miniaplicación web.
*   **Vercel:** Plataforma de despliegue.
*   **Netlify:** Plataforma de despliegue.
*   **Supabase:** (Mencionado en las mejoras futuras para la gestión de cuestionarios).

## 📚 Contexto Formativo

Este proyecto se enmarca en el curso/módulo **INTELIGENCIA ARTIFICIAL GENERATIVA Y MEJORA DE LA PRODUCTIVIDAD**, con fecha 01/06/2026, realizado por Francisco y Miguel. El objetivo fue diseñar y publicar una miniaplicación web útil para el entorno educativo utilizando herramientas de IA o No Code, y prepararla para su despliegue.

---

<p align="center">
  <sub>Documentado por **migueljerico@gmail.com** · 2026</sub>
</p>
