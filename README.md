# 🎓 Estudio360 Smart Learn — Documentación del Proceso

![Lovable](https://img.shields.io/badge/Lovable-No%20Code%20%2F%20Low%20Code-FF4F64?style=for-the-badge)
![Vercel](https://img.shields.io/badge/Vercel-Desplegado-000000?style=for-the-badge&logo=vercel&logoColor=white)
![Netlify](https://img.shields.io/badge/Netlify-Desplegado-00C7B7?style=for-the-badge&logo=netlify&logoColor=white)
![Supabase](https://img.shields.io/badge/Supabase-Backend-3ECF8E?style=for-the-badge&logo=supabase&logoColor=white)
![Estado](https://img.shields.io/badge/Estado-Completado-4CAF50?style=for-the-badge)
![Tipo](https://img.shields.io/badge/Práctica-IA%20Generativa%20No%20Code-FF6B6B?style=for-the-badge)
![Licencia](https://img.shields.io/badge/Licencia-MIT-FF4F64?style=for-the-badge)

> **Ejercicio Práctico — IA Generativa y Mejora de la Productividad**
> Documentación completa del proceso de creación de **Estudio360 Smart Learn** con Lovable

---

## 🔗 Acceso / Demo

| Plataforma | Enlace |
|---|---|
| **Vercel** | [estudio-360-smart-learn-vercel.vercel.app](https://estudio-360-smart-learn-vercel.vercel.app/) |
| **Netlify** | [estudio360.netlify.app](https://estudio360.netlify.app/) |

**Repos de código fuente:**
- [Despliegue Vercel](https://github.com/migueljerico/estudio-360-smart-learn-vercel)
- [Despliegue Netlify](https://github.com/migueljerico/estudio-360-smart-learn-netlify)

---

## 📋 Descripción

Este repositorio documenta el proceso completo de creación de **Estudio360 Smart Learn**, una plataforma educativa desarrollada íntegramente con **Lovable** (herramienta de IA generativa no-code / low-code) para profesorado y alumnado de Educación Primaria.

El proyecto resuelve una necesidad concreta en el entorno educativo: permitir a los profesores crear, organizar y asignar contenido de repaso (flashcards y cuestionarios) de forma rápida, mientras que los alumnos pueden autoevaluarse de manera personalizada y seguir su propio progreso de aprendizaje. La aplicación implementa un sistema de roles que garantiza que cada alumno solo acceda a su información y al contenido asignado por su profesor.

Este repositorio recoge los prompts utilizados, las iteraciones realizadas durante la generación con IA, las decisiones técnicas tomadas durante el despliegue en Vercel y Netlify, y una reflexión crítica sobre las capacidades y limitaciones del uso de IA generativa para la creación de aplicaciones web funcionales.

---

## ✨ Funcionalidades

### 👩‍🏫 Funcionalidades para el Profesorado

| Funcionalidad | Descripción |
|---|---|
| Creación de flashcards | Crear, editar y eliminar tarjetas de repaso organizadas por tema o unidad didáctica |
| Gestión de quizzes | Crear cuestionarios con múltiples preguntas y opciones de respuesta |
| Asignación de contenido | Asignar decks de flashcards y quizzes a clases o grupos específicos de alumnos |
| Estadísticas de clase | Visualizar resultados agregados por alumno y por pregunta para identificar debilidades |
| Detección de fallos | Identificar automáticamente las preguntas con mayor tasa de error para refuerzo |
| Reutilización de contenido | Publicar y duplicar contenido existente para evitar redundancias |

### 🎒 Funcionalidades para el Alumnado

| Funcionalidad | Descripción |
|---|---|
| Autoevaluaciones | Realizar quizzes cortos y repetibles para medir su comprensión |
| Seguimiento de progreso | Consultar aciertos, errores y temas pendientes de forma visual |
| Repaso inteligente | Repasar tarjetas y preguntas falladas con mayor frecuencia de forma prioritaria |
| Acceso seguro | Acceder exclusivamente a su información y al contenido asignado por su profesor |
| Feedback inmediato | Recibir resultados y explicaciones al instar después de completar cada quiz |

---

## ⚙️ Instalación

Este repositorio es de **documentación** y no contiene código ejecutable. Los repositorios con el código fuente de la aplicación son:

- [Repositorio Vercel](https://github.com/migueljerico/estudio-360-smart-learn-vercel)
- [Repositorio Netlify](https://github.com/migueljerico/estudio-360-smart-learn-netlify)

### Clonar la documentación

```bash
git clone https://github.com/migueljerico/estudio-360-smart-learn-documentation.git
cd estudio-360-smart-learn-documentation
```

### Clonar el código fuente (despliegue Vercel)

```bash
git clone https://github.com/migueljerico/estudio-360-smart-learn-vercel.git
cd estudio-360-smart-learn-vercel
npm install
```

### Ejecutar en desarrollo

```bash
npm run dev
```

La aplicación estará disponible en `http://localhost:5173`.

---

## 🚀 Uso

### Generación con Lovable

La aplicación fue generada a partir del siguiente prompt inicial en Lovable:

```
Crea una aplicación web educativa llamada Estudio 360.
La app debe tener dos roles principales: Profesor y Alumno.

Objetivo:
- Los profesores creen, editen y asignen contenido educativo
- Los alumnos realicen autoevaluaciones personalizadas
- Cada alumno vea únicamente sus propios datos, progreso y resultados

Funcionalidades para Profesor:
Crear/editar/eliminar flashcards y quizzes, organizar por curso/tema/unidad,
asignar a alumnos o grupos, ver progreso individual y estadísticas de clase,
detectar preguntas con más fallos, duplicar contenido existente.

Funcionalidades para Alumno:
Ver contenido asignado, estudiar flashcards en modo repaso,
realizar quizzes de autoevaluación, ver resultados inmediatos,
consultar historial de intentos y métricas personales,
repasar solo tarjetas o preguntas falladas.

Diseño: interfaz moderna, limpia y minimalista. Muy fácil de usar
en móvil y escritorio. Colores agradables, buena jerarquía visual.

Modelo de datos: Usuarios, Roles, Clases, Alumnos, Profesores,
Decks de flashcards, Quizzes, Preguntas, Respuestas, Intentos,
Progreso por usuario, Asignaciones de contenido.

Reglas: Un alumno solo puede ver sus propios datos.
Un profesor puede ver el contenido y progreso de sus alumnos.
```

### Iteración 1 — Traducción al castellano

**Problema detectado:** Lovable generó las tarjetas y cuestionarios en inglés (`decks`, `quizzes`).

**Solución aplicada:** Se modificó el contenido a castellano para adaptarlo al público objetivo (alumnado de Educación Primaria en España).

---

## 📁 Estructura del Proyecto

```
estudio-360-smart-learn-documentation/
├── README.md                  # Documentación principal del proceso
├── LICENSE                    # Licencia MIT
└── screenshots/               # Capturas de la aplicación (referenciadas externamente)
```

---

## 🛠️ Tecnologías

| Herramienta | Versión / Detalle | Uso en el Proyecto |
|---|---|---|
| **Lovable** | Plataforma IA no-code | Generación completa de la aplicación web a partir de prompts en lenguaje natural |
| **React** | Framework UI | Framework de interfaz de usuario generado por Lovable |
| **Vite** | Bundler / Dev server | Sistema de construcción y desarrollo del frontend (requiere preset `vercel` en `vite.config.ts`) |
| **Vercel** | Plataforma de despliegue | Hosting y despliegue continuo de la versión principal |
| **Netlify** | Plataforma de despliegue | Despliegue alternativo con agente IA integrado para corrección automática |
| **Supabase** | Backend as a Service | Autenticación de usuarios, base de datos relacional y gestión de roles |
| **TypeScript** | Lenguaje tipado | Utilizado en el código generado para mayor robustez |
| **Tailwind CSS** | Framework CSS | Estilos del frontend generados por Lovable |

---

## 📸 Vista Previa

> **Nota:** Las capturas de pantalla se encuentran en repositorios externos. Consulta los enlaces de la sección de Demo para ver la aplicación en funcionamiento.

---

## 🔍 Proceso de Despliegue

### Despliegue en Vercel

El despliegue inicial presentó un **error 404**. Tras análisis del código generado, se identificó que el problema era un valor incorrecto del preset en `vite.config.ts` (estaba configurado como `netlify` en lugar de `vercel`). Una vez corregido el preset, el despliegue funcionó correctamente.

| Plataforma | Resultado | Observación |
|---|---|---|
| **Vercel** | ✅ Exitoso | Requirió corrección manual del preset en `vite.config.ts` |
| **Netlify** | ✅ Exitoso | El agente IA de Netlify detectó y corrigió el código automáticamente |

### Despliegue en Netlify

El despliegue en Netlify fue exitoso desde el primer intento. El agente IA de Netlify analizó el código durante el proceso de despliegue y realizó correcciones automáticas, lo que facilitó significativamente la depuración.

---

## 💡 Reflexión Crítica

### Facilidades y Dificultades

La creación de la aplicación con Lovable fue la parte más ágil del proceso, destacando la eficiencia de la IA generativa para producir una aplicación funcional con roles, autenticación y una interfaz completa en muy poco tiempo. La mayor dificultad fue el despliegue en Vercel, que resultó menos intuitivo para la depuración en comparación con Netlify.

### Riesgos y Limitaciones del Desarrollo con IA Generativa

| Riesgo | Descripción |
|---|---|
| **Falta de control** | La facilidad para implementar lógica sin comprensión profunda dificulta la corrección de fallos futuros |
| **Alucinaciones** | La IA puede generar soluciones incorrectas o ignorar aspectos críticos de seguridad |
| **Visión limitada** | Pérdida de eficiencia en arquitecturas complejas o altamente escalables |

> **Conclusión:** La IA generativa es un excelente copiloto para acelerar el desarrollo, pero requiere supervisión humana constante para asegurar la calidad, la seguridad y la robustez del producto final.

---

## 🔮 Mejoras Futuras

1. **Generación de cuestionarios asistida por IA** — El profesor introduce un tema y la app genera un borrador de preguntas automáticamente
2. **Dashboards de análisis por rol** — Visualizaciones específicas para profesores (métricas de clase) y alumnos (seguimiento personal)
3. **Notificaciones automáticas** — Avisos a profesores y alumnos sobre asignaciones pendientes y feedback recibido

---

## 📚 Contexto Formativo

Este proyecto forma parte del módulo **Inteligencia Artificial Generativa y Mejora de la Productividad** (junio 2026). El objetivo fue diseñar, construir y desplegar una aplicación web útil para el entorno educativo utilizando herramientas de IA generativa y no-code, documentando todo el proceso de creación y las decisiones técnicas tomadas.

Proyecto realizado en equipo por **Francisco y Miguel**.

---

<p align="center">Creado por @migueljerico y documentado por OpenCode Zen (MiMo-V2.5 (free)) · 2026</p>