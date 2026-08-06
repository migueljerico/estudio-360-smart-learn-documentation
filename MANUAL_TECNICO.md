# Manual Técnico — Estudio360 Smart Learn

> **Repositorio documentación:** `migueljerico/estudio-360-smart-learn-documentation`  
> **Repositorios de código fuente:**  
> - [estudio-360-smart-learn-vercel](https://github.com/migueljerico/estudio-360-smart-learn-vercel)  
> - [estudio-360-smart-learn-netlify](https://github.com/migueljerico/estudio-360-smart-learn-netlify)  
> **Licencia:** MIT  
> **Autor:** Miguel Jericó  

---

## 1. Arquitectura General del Sistema

### 1.1 Stack Tecnológico

| Capa | Tecnología | Rol |
|------|-----------|-----|
| **Frontend / Presentación** | Lovable (Low-Code/No-Code) | Generación y mantenimiento de la interfaz de usuario |
| **Backend / Lógica de negocio** | Supabase | API, autenticación, base de datos y reglas de seguridad (RLS) |
| **Despliegue / Hosting** | Vercel + Netlify | Hospedaje de la aplicación frontend en producción |

### 1.2 Diagrama de Arquitectura en Capas

```
┌─────────────────────────────────────────────────────────────────────┐
│                        CAPA DE PRESENTACIÓN                        │
│                                                                     │
│  ┌───────────────────────┐      ┌────────────────────────────────┐ │
│  │    Interfaz Lovable   │      │   Despliegues de Producción    │ │
│  │  (Componentes React   │      │  ┌──────────┐ ┌─────────────┐  │ │
│  │   + Tailwind CSS)     │      │  │  Vercel  │ │   Netlify   │  │ │
│  │                       │◄────►│  │(primario)│ │(alternativo)│  │ │
│  │  - Rutas por rol      │      │  └──────────┘ └─────────────┘  │ │
│  │  - Formularios        │      └────────────────────────────────┘ │
│  │  - Dashboards         │                                         │
│  │  - Flashcards UI      │                                         │
│  │  - Quiz Engine        │                                         │
│  └───────────┬───────────┘                                         │
│              │                                                      │
│              │ HTTPS / REST API + Realtime                          │
│              ▼                                                      │
├─────────────────────────────────────────────────────────────────────┤
│                      CAPA DE LÓGICA / BACKEND                      │
│                                                                     │
│  ┌──────────────────────────────────────────────────────────────┐   │
│  │                        SUPABASE                              │   │
│  │                                                              │   │
│  │  ┌──────────────┐  ┌──────────────┐  ┌──────────────────┐  │   │
│  │  │ Autenticación │  │   Edge       │  │  Row Level       │  │   │
│  │  │ (Auth)        │  │ Functions    │  │  Security (RLS)  │  │   │
│  │  │ - Login       │  │ (Serverless) │  │  - Aislamiento   │  │   │
│  │  │ - Registro    │  │ - Lógica     │  │    por usuario   │  │   │
│  │  │ - Sesiones    │  │   personali- │  │  - Permisos      │  │   │
│  │  │ - Roles       │  │   zada       │  │    por rol       │  │   │
│  │  └──────────────┘  └──────────────┘  └──────────────────┘  │   │
│  │                                                              │   │
│  │  ┌──────────────┐  ┌──────────────┐                         │   │
│  │  │   Storage    │  │  Realtime    │                         │   │
│  │  │ (Archivos)   │  │ (Websockets) │                         │   │
│  │  └──────────────┘  └──────────────┘                         │   │
│  └──────────────────────────┬───────────────────────────────────┘   │
│                             │                                       │
│                             │ Conexión directa                      │
│                             ▼                                       │
├─────────────────────────────────────────────────────────────────────┤
│                       CAPA DE DATOS                                 │
│                                                                     │
│  ┌──────────────────────────────────────────────────────────────┐   │
│  │              BASE DE DATOS PostgreSQL (Supabase)             │   │
│  │                                                              │   │
│  │  Tablas principales (inferidas):                             │   │
│  │  ┌────────────┐  ┌─────────────┐  ┌──────────────────────┐ │   │
│  │  │ profiles   │  │ flashcards  │  │        quizzes       │ │   │
│  │  │ (usuarios) │  │ (tarjetas)  │  │ (cuestionarios)      │ │   │
│  │  └────────────┘  └─────────────┘  └──────────────────────┘ │   │
│  │                                                              │   │
│  │  ┌────────────────┐  ┌─────────────┐  ┌──────────────────┐ │   │
│  │  │ assignments    │  │  progress   │  │  results         │ │   │
│  │  │ (asignaciones) │  │ (progreso)  │  │ (resultados)     │ │   │
│  │  └────────────────┘  └─────────────┘  └──────────────────┘ │   │
│  └──────────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────────┘
```

### 1.3 Diagrama de Flujo de Autenticación

```
┌─────────┐         ┌──────────────┐         ┌──────────────────┐
│ Usuario │         │  Frontend    │         │    Supabase      │
│         │  Login  │  (Lovable)   │  Auth   │    Auth API      │
└────┬────┘────────►└──────┬───────┘────────►└────────┬─────────┘
     │                     │                          │
     │                     │    Token JWT             │
     │                     │◄─────────────────────────│
     │                     │                          │
     │                     │  Consulta con JWT        │
     │                     │─────────────────────────►│
     │                     │                          │
     │                     │    RLS Filter            │
     │                     │◄─────────────────────────│
     │                     │  (Solo datos propios)    │
     │  Renderizado con    │                          │
     │  datos filtrados    │                          │
     │◄────────────────────│                          │
```

---

## 2. Descripción de Módulos y Componentes Principales

### 2.1 Estructura del Repositorio de Documentación

```
migueljerico/estudio-360-smart-learn-documentation/
├── README.md                          # Documentación principal del proceso
├── LICENSE                            # Licencia MIT
├── screenshots/                       # Capturas de la aplicación
│   └── Captura_Estudio360_Lovable.png
└── MANUAL_TECNICO.md                  # Este documento
```

**Responsabilidad de este repositorio:**  
Este repositorio NO contiene código ejecutable. Su propósito es documentar el proceso completo de creación de la aplicación Estudio360 Smart Learn, incluyendo prompts utilizados, iteraciones, decisiones técnicas y reflexión crítica sobre el uso de IA generativa.

### 2.2 Repositorios de Código Fuente

#### 2.2.1 `estudio-360-smart-learn-vercel`

| Atributo | Valor |
|----------|-------|
| **Propósito** | Despliegue de la aplicación en Vercel |
| **URL producción** | https://estudio-360-smart-learn-vercel.vercel.app/ |
| **Plataforma de generación** | Lovable |
| **Framework inferido** | React + Vite + TypeScript + Tailwind CSS |

#### 2.2.2 `estudio-360-smart-learn-netlify`

| Atributo | Valor |
|----------|-------|
| **Propósito** | Despliegue alternativo en Netlify |
| **URL producción** | https://estudio360.netlify.app/ |
| **Plataforma de generación** | Lovable |
| **Framework inferido** | React + Vite + TypeScript + Tailwind CSS |

### 2.3 Módulos Funcionales de la Aplicación

#### 2.3.1 Módulo de Autenticación y Gestión de Usuarios

| Aspecto | Detalle |
|---------|---------|
| **Responsabilidad** | Registro, login, gestión de sesiones, control de roles |
| **Roles soportados** | `profesor`, `alumno` |
| **Proveedor** | Supabase Auth |
| **Métodos de login** | Email/password (inferido) |

#### 2.3.2 Módulo de Gestión de Flashcards (Profesorado)

| Aspecto | Detalle |
|---------|---------|
| **Responsabilidad** | CRUD de tarjetas de estudio |
| **Funcionalidades** | Crear, editar, eliminar flashcards |
| **Organización** | Por curso → tema → unidad |
| **Asignación** | A alumnos individuales o grupos |
| **Ciclo de vida** | Borrador → Publicado → Archivado |

#### 2.3.3 Módulo de Gestión de Quizzes (Profesorado)

| Aspecto | Detalle |
|---------|---------|
| **Responsabilidad** | CRUD de cuestionarios y preguntas |
| **Funcionalidades** | Crear, editar, eliminar quizzes |
| **Organización** | Por tema o unidad |
| **Asignación** | A alumnos o grupos específicos |
| **Tipos de pregunta** | Opción múltiple, verdadero/falso (inferido) |

#### 2.3.4 Módulo de Autoevaluación (Alumnado)

| Aspecto | Detalle |
|---------|---------|
| **Responsabilidad** | Realización de quizzes asignados |
| **Funcionalidades** | Evaluar respuestas, calcular puntuación |
| **Feedback** | Inmediato después de cada quiz |
| **Repetibilidad** | Los quizzes pueden repetirse |

#### 2.3.5 Módulo de Seguimiento de Progreso (Alumnado)

| Aspecto | Detalle |
|---------|---------|
| **Responsabilidad** | Tracking individual del rendimiento |
| **Métricas** | Aciertos, errores, temas pendientes |
| **Repaso inteligente** | Priorización de tarjetas falladas con mayor frecuencia |
| **Visibilidad** | Solo datos propios del alumno (RLS) |

#### 2.3.6 Módulo de Estadísticas y Analíticas (Profesorado)

| Aspecto | Detalle |
|---------|---------|
| **Responsabilidad** | Visualización de rendimiento colectivo |
| **Métricas** | Resultados agregados por alumno y por pregunta |
| **Detección** | Preguntas con mayor tasa de fallo |
| **Uso** | Identificar áreas de refuerzo |

---

## 3. Tablas de Base de Datos (Inferidas)

> **Nota:** Las tablas以下 se infieren a partir de las funcionalidades documentadas. Para la definición exacta, consulte el repositorio de código fuente y el panel de Supabase.

| Tabla | Descripción | Relaciones Clave |
|-------|-------------|------------------|
| `profiles` | Perfiles de usuario (profesor/alumno) | FK → `auth.users.id` |
| `classes` | Clases o grupos creados por profesores | FK → `profiles.id` (profesor) |
| `class_members` | Relación alumno-clase | FK → `classes.id`, `profiles.id` |
| `flashcards` | Tarjetas de estudio | FK → `profiles.id` (creador), tema/unidad |
| `quizzes` | Cuestionarios | FK → `profiles.id` (creador) |
| `quiz_questions` | Preguntas dentro de un quiz | FK → `quizzes.id` |
| `assignments` | Asignaciones de contenido a alumnos/grupos | FK → `quizzes.id`/`flashcards.id`, `classes.id` |
| `quiz_results` | Resultados de intentos de quiz | FK → `quizzes.id`, `profiles.id` (alumno) |
| `flashcard_progress` | Progreso individual por flashcard | FK → `flashcards.id`, `profiles.id` |

---

## 4. Variables de Entorno

### 4.1 Supabase (Backend)

| Variable | Valor de ejemplo | Obligatoria | Descripción |
|----------|-----------------|-------------|-------------|
| `SUPABASE_URL` | `https://xxxxx.supabase.co` | **Sí** | URL del proyecto Supabase |
| `SUPABASE_ANON_KEY` | `eyJhbGciOiJIUzI1NiIs...` | **Sí** | Clave pública (anon) de Supabase |
| `SUPABASE_SERVICE_ROLE_KEY` | `eyJhbGciOiJIUzI1NiIs...` | No* | Clave con privilegios administrativos (*solo server-side) |

### 4.2 Despliegue en Vercel

| Variable | Valor de ejemplo | Obligatoria | Descripción |
|----------|-----------------|-------------|-------------|
| `VITE_SUPABASE_URL` | `https://xxxxx.supabase.co` | **Sí** | URL de Supabase expuesta al frontend |
| `VITE_SUPABASE_ANON_KEY` | `eyJhbGciOiJIUzI1NiIs...` | **Sí** | Clave anon expuesta al frontend |

### 4.3 Despliegue en Netlify

| Variable | Valor de ejemplo | Obligatoria | Descripción |
|----------|-----------------|-------------|-------------|
| `SUPABASE_URL` | `https://xxxxx.supabase.co` | **Sí** | URL de Supabase |
| `SUPABASE_ANON_KEY` | `eyJhbGciOiJIUzI1NiIs...` | **Sí** | Clave anon de Supabase |
| `VITE_*` | Prefijo alternativo | **Sí** | Variables del lado del cliente (Vite) |

> **Nota:** Las variables exactas pueden variar según la configuración de Lovable. Consulte el panel de variables en Vercel/Netlify y las variables definidas en el archivo `.env.example` del repositorio de código fuente.

---

## 5. Guía de Despliegue Paso a Paso

### 5.1 Desarrollo con Lovable

```
┌──────────────────────────────────────────────────────────────┐
│                    FLUJO DE DESARROLLO                        │
│                                                              │
│  1. Prompt Inicial                                           │
│     │                                                        │
│     ▼                                                        │
│  2. Generación Automática (Lovable)                          │
│     │  - Código fuente React + TypeScript                    │
│     │  - Configuración de Supabase                           │
│     │  - UI con Tailwind CSS                                 │
│     ▼                                                        │
│  3. Iteración y Refinamiento                                 │
│     │  - Prompts adicionales                                 │
│     │  - Corrección de errores                               │
│     │  - Ajustes de diseño                                   │
│     ▼                                                        │
│  4. Exportación de Código                                    │
│     │  - Repositorio GitHub                                  │
│     ▼                                                        │
│  5. Despliegue (Vercel / Netlify)                            │
└──────────────────────────────────────────────────────────────┘
```

### 5.2 Configuración de Supabase

1. **Crear proyecto en Supabase:**
   - Acceder a [supabase.com](https://supabase.com)
   - Crear nuevo proyecto
   - Anotar URL y clave `anon`

2. **Configurar Autenticación:**
   - Habilitar proveedores de auth (Email/Password)
   - Configurar plantillas de email (opcional)

3. **Crear esquema de base de datos:**
   - Ejecutar migraciones SQL o usar el Editor SQL de Supabase
   - Crear tablas según el modelo de datos

4. **Configurar Row Level Security (RLS):**
   ```sql
   -- Ejemplo: política para que cada alumno solo vea sus resultados
   ALTER TABLE quiz_results ENABLE ROW LEVEL SECURITY;

   CREATE POLICY "Alumnos ven sus propios resultados"
     ON quiz_results
     FOR SELECT
     USING (auth.uid() = user_id);

   -- Ejemplo: política para que profesores vean resultados de su clase
   CREATE POLICY "Profesores ven resultados de su clase"
     ON quiz_results
     FOR SELECT
     USING (
       EXISTS (
         SELECT 1 FROM class_members
         WHERE class_members.class_id = quiz_results.class_id
         AND class_members.teacher_id = auth.uid()
       )
     );
   ```

### 5.3 Despliegue en Vercel (Primario)

1. **Conectar repositorio GitHub:**
   - Ir a [vercel.com/new](https://vercel.com/new)
   - Importar repositorio `estudio-360-smart-learn-vercel`
   - Seleccionar framework: **Vite** (detectado automáticamente)

2. **Configurar Variables de Entorno:**
   ```
   VITE_SUPABASE_URL=https://tu-proyecto.supabase.co
   VITE_SUPABASE_ANON_KEY=tu-clave-anon-aqui
   ```

3. **Configurar Build:**
   | Parámetro | Valor |
   |-----------|-------|
   | Build Command | `npm run build` |
   | Output Directory | `dist` |
   | Install Command | `npm install` |

4. **Deploy:**
   - Clic en "Deploy"
   - Verificar despliegue exitoso
   - Asignar dominio personalizado (opcional)

### 5.4 Despliegue en Netlify (Alternativo)

1. **Conectar repositorio GitHub:**
   - Ir a [app.netlify.com](https://app.netlify.com)
   - "Add new site" → "Import an existing project"
   - Seleccionar repositorio `estudio-360-smart-learn-netlify`

2. **Configurar Variables de Entorno:**
   ```
   SUPABASE_URL=https://tu-proyecto.supabase.co
   SUPABASE_ANON_KEY=tu-clave-anon-aqui
   ```

3. **Configurar Build:**
   | Parámetro | Valor |
   |-----------|-------|
   | Build Command | `npm run build` |
   | Publish Directory | `dist` |

4. **Deploy:**
   - Clic en "Deploy site"
   - Verificar despliegue exitoso

### 5.5 Verificación Post-Despliegue

| Verificación | Cómo |
|--------------|------|
| La app carga correctamente | Abrir URL de producción en navegador |
| Login funciona | Registrar usuario de prueba (profesor y alumno) |
| Conexión a Supabase | Verificar en pestaña Network del DevTools que no hay errores 401/403 |
| RLS activo | Verificar que un alumno no puede ver datos de otro alumno |
| Quizzes asignados aparecen | Crear quiz como profesor, asignar a alumno, verificar que aparece |

---

## 6. Roles y Permisos

### 6.1 Matriz de Permisos

| Recurso | Profesor | Alumno |
|---------|----------|--------|
| Crear flashcards | ✅ | ❌ |
| Editar flashcards propios | ✅ | ❌ |
| Eliminar flashcards propios | ✅ | ❌ |
| Crear quizzes | ✅ | ❌ |
| Editar quizzes propios | ✅ | ❌ |
| Eliminar quizzes propios | ✅ | ❌ |
| Asignar contenido a alumnos/grupos | ✅ | ❌ |
| Ver estadísticas de clase | ✅ | ❌ |
| Ver preguntas con mayor tasa de fallo | ✅ | ❌ |
| Ver flashcards asignadas | ❌ | ✅ |
| Realizar quizzes asignados | ❌ | ✅ |
| Ver propio progreso | ❌ | ✅ |
| Ver propio historial de resultados | ❌ | ✅ |
| Repasar flashcards falladas | ❌ | ✅ |
| Ver datos de otros alumnos | ❌ | ❌ (RLS) |

---

## 7. Limitaciones Conocidas y Posibles Mejoras Futuras

### 7.1 Limitaciones Actuales

| # | Limitación | Impacto | Notas |
|---|-----------|---------|-------|
| L1 | **Repositorio de documentación sin código ejecutable** | Medio | Este repo contiene solo documentación; el código está en repos separados |
| L2 | **Generación por Low-Code/No-Code (Lovable)** | Medio | La lógica compleja puede ser difícil de personalizar fuera de la plataforma |
| L3 | **Dependencia de Lovable** | Alto | Las actualizaciones de la plataforma pueden afectar la mantenibilidad |
| L4 | **Sin tests automatizados visibles** | Medio | No se evidencian pruebas unitarias o de integración en el proceso documentado |
| L5 | **Despliegue dual sin sincronización** | Bajo | Vercel y Netlify son independientes; la sincronización depende del flujo de CI/CD |
| L6 | **RLS y seguridad dependen de configuración manual** | Alto | Errores en políticas RLS pueden exponer datos entre usuarios |
| L7 | **Sin documentación de API explícita** | Medio | Las APIs de Supabase se generan automáticamente; no hay OpenAPI/Swagger |

### 7.2 Mejoras Futuras Propuestas

| # | Mejora | Prioridad | Complejidad | Descripción |
|---|--------|-----------|-------------|-------------|
| M1 | **Migración a código propio** | Alta | Alta | Exportar completamente el código de Lovable y mantenerlo manualmente |
| M2 | **Tests automatizados** | Alta | Media | Implementar pruebas unitarias (Vitest) y E2E (Playwright/Cypress) |
| M3 | **CI/CD unificado** | Media | Media | Configurar pipeline único con GitHub Actions que despliegue a ambos proveedores |
| M4 | **Documentación de API** | Media | Baja | Generar documentación OpenAPI de los endpoints de Supabase |
| M5 | **Sistema de notificaciones** | Media | Media | Email/push para notificar asignaciones nuevas y resultados |
| M6 | **Modo offline / PWA** | Baja | Alta | Permitir repaso de flashcards sin conexión a internet |
| M7 | **Exportación de datos** | Baja | Baja | Permitir exportar progreso y resultados en CSV/PDF |
| M8 | **Internacionalización (i18n)** | Baja | Media | Soporte multiidioma para uso en otros países hispanohablantes |
| M9 | **Panel de administración** | Media | Alta | Gestión de usuarios, configuración del sistema y auditoría |
| M10 | **Monitoreo y métricas** | Media | Baja | Integrar Sentry para errores y analytics para uso |

### 7.3 Deuda Técnica Identificada

```
┌─────────────────────────────────────────────────────────────────┐
│                    PRIORIDAD DE MEJORAS                          │
│                                                                 │
│  ALTA                                                           │
│  ├── M1: Migración a código propio                              │
│  ├── M2: Tests automatizados                                    │
│  └── Seguridad: Verificar políticas RLS exhaustivamente        │
│                                                                 │
│  MEDIA                                                          │
│  ├── M3: CI/CD unificado                                        │
│  ├── M4: Documentación de API                                   │
│  ├── M5: Notificaciones                                         │
│  └── M9: Panel de administración                                │
│                                                                 │
│  BAJA                                                           │
│  ├── M6: Modo offline / PWA                                     │
│  ├── M7: Exportación de datos                                   │
│  ├── M8: Internacionalización                                   │
│  └── M10: Monitoreo y métricas                                  │
└─────────────────────────────────────────────────────────────────┘
```

---

## 8. Decisiones Técnicas Documentadas

### 8.1 ¿Por qué Lovable?

Lovable se eligió como plataforma de generación como parte del ejercicio práctico de **IA Generativa y Mejora de la Productividad**. Ventajas observadas:

| Ventaja | Descripción |
|---------|-------------|
| Generación rápida | La aplicación completa se generó a partir de un prompt detallado |
| Stack moderno | React + TypeScript + Tailwind CSS + Vite |
| Integración nativa | Conexión directa con Supabase |
| Exportación de código | Posibilidad de exportar el código generado a GitHub |

### 8.2 ¿Por qué despliegue dual (Vercel + Netlify)?

| Razón | Detalle |
|-------|---------|
| Redundancia | Si un proveedor falla, el otro sigue activo |
| Comparativa de rendimiento | Evaluar tiempos de carga y comportamiento en ambos |
| Ejercicio educativo | Explorar diferentes plataformas de despliegue |
| Flexibilidad | Cada plataforma tiene fortalezas distintas (Edge functions, forms, etc.) |

---

## 9. Recursos y Enlaces

| Recurso | URL |
|---------|-----|
| App en Vercel (producción) | https://estudio-360-smart-learn-vercel.vercel.app/ |
| App en Netlify (producción) | https://estudio360.netlify.app/ |
| Repo código Vercel | https://github.com/migueljerico/estudio-360-smart-learn-vercel |
| Repo código Netlify | https://github.com/migueljerico/estudio-360-smart-learn-netlify |
| Repo documentación | https://github.com/migueljerico/estudio-360-smart-learn-documentation |
| Supabase Dashboard | https://supabase.com/dashboard |
| Vercel Dashboard | https://vercel.com/dashboard |
| Netlify Dashboard | https://app.netlify.com |
| Lovable | https://lovable.dev |

---

## 10. Información de Contacto y Licencia

- **Autor:** Miguel Jericó
- **Licencia:** MIT License (Copyright © 2026)
- **Uso permitido:** Libre uso, modificación y distribución según los términos de la licencia MIT

---

> **Última actualización:** Documento generado a partir del análisis del repositorio `migueljerico/estudio-360-smart-learn-documentation`.  
> **Nota:** Para información precisa sobre el código fuente, consulte los repositorios de despliegue enlazados en la sección 9.