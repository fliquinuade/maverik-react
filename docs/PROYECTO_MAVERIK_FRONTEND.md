# PROYECTO MAVERIK - FRONTEND

## Resumen ejecutivo

**Maverik** es una aplicación web de asesoramiento financiero que permite a los usuarios registrarse, completar un perfil de riesgo y recibir recomendaciones de inversión personalizadas a través de un sistema de chat interactivo. El frontend está construido con React 18 + Vite y completamente dockerizado para facilitar el desarrollo y despliegue.

### Características principales

- 🎯 **Sistema de onboarding** con formulario multi-paso para perfilado de usuarios
- 💬 **Chat de asesoría** interactivo con IA/backend especializado
- 🔐 **Autenticación** con tokens JWT y almacenamiento en session
- 🎨 **UI moderna** con Bootstrap 5, temas dinámicos y componentes reutilizables
- 📱 **Responsive design** optimizado para móvil y desktop
- 🐳 **Dockerización completa** con multi-stage builds para desarrollo y producción
- ⚡ **Performance optimizado** con Vite, lazy loading y compresión

## Documentación técnica detallada

Este documento resume en alto nivel en qué consiste la aplicación, cómo está estructurado el frontend, los componentes principales, los endpoints que consume, y consideraciones importantes para continuar el desarrollo.

### Cómo ejecutar (desarrollo)

#### Método Docker (Recomendado)

```bash
# 1. Configurar variables de entorno
cp .env.example .env
# Editar .env con la URL de tu API

# 2. Ejecutar con Docker Compose
docker-compose --profile dev up --build

# 3. Acceder a la aplicación
# http://localhost:5173
```

#### Método tradicional (Node.js local)

```bash
# 1. Instalar dependencias
npm install

# 2. Configurar variables de entorno
cp .env.example .env

# 3. Iniciar servidor de desarrollo
npm run dev

# 4. Acceder a la aplicación
# http://localhost:5173
```

**Variables de entorno requeridas:**
- `VITE_API_URL` - URL base de la API (ej: `http://localhost:8000/api`)
- `VITE_BASE_URL` - Base path para deployment (opcional)

Ver `docs/docker.md` para más detalles sobre Docker.

El proyecto usa `VITE_BASE_URL` (en `vite.config.js`) para configurar el base path en despliegue, y `VITE_API_URL` (en `src/services/shared/config.js`) como URL base para las llamadas a la API.

## Arquitectura y stack tecnológico

### Stack principal
- **React 18** - Biblioteca de interfaz de usuario
- **Vite** - Build tool y servidor de desarrollo
- **Bootstrap 5 + React Bootstrap** - Framework CSS y componentes
- **SCSS** - Preprocesador CSS para estilos personalizados
- **Axios** - Cliente HTTP para comunicación con API
- **React Router DOM** - Enrutamiento del lado del cliente
- **React Hook Form + Yup** - Manejo y validación de formularios

### Librerías especializadas
- **glightbox** - Lightbox para galerías de imágenes
- **isotope-layout** - Layouts dinámicos y filtrado
- **jarallax** - Efectos de parallax
- **swiper** - Carruseles y sliders
- **react-toastify** - Sistema de notificaciones
- **react-countup** - Animaciones de contadores
- **bs-stepper** - Componente de pasos/wizard

### Herramientas de desarrollo
- **ESLint** - Linting de código
- **Prettier** - Formateo de código
- **Docker** - Containerización para desarrollo y producción

### Estructura principal (resumen)

```
src/
├── 📄 App.jsx, main.jsx           # Punto de entrada y componente raíz
├── 📁 assets/                     # Recursos estáticos
│   ├── data/                      # Datos mock y configuraciones
│   ├── images/                    # Imágenes y logos
│   └── scss/                      # Estilos SCSS (variables, temas)
├── 📁 components/                 # Componentes reutilizables
│   ├── cards/                     # Componentes tipo tarjeta
│   ├── footer/                    # Componentes de footer (8 variantes)
│   ├── form/                      # Inputs y componentes de formulario
│   └── topbar/                    # Navegación y header
├── 📁 helpers/                    # Utilidades específicas del dominio
├── 📁 hooks/                      # Hooks personalizados de React
├── 📁 layouts/                    # Layouts de páginas
│   ├── DefaultLayout/             # Layout principal
│   ├── AccountLayout/             # Layout para cuenta de usuario
│   ├── AuthLayout/                # Layout para autenticación
│   ├── BlogLayout/                # Layout para blog
│   └── ShopLayout/                # Layout para tienda
├── 📁 pages/                      # Páginas de la aplicación
│   ├── home.jsx                   # Página principal
│   ├── signin.jsx, signup.jsx     # Autenticación
│   ├── wizard.jsx                 # Onboarding multi-paso
│   ├── chat.jsx                   # Chat de asesoría
│   └── other-pages/               # Páginas adicionales
├── 📁 routes/                     # Configuración de rutas
├── 📁 services/                   # Cliente HTTP y servicios de API
│   ├── users.js                   # Servicios de usuario
│   ├── copilot_sessions.js        # Servicios de asesoría
│   └── shared/                    # Utilidades compartidas
├── 📁 states/                     # Contextos y estado global
│   ├── useAuthContext.jsx         # Contexto de autenticación
│   ├── useLayoutContext.jsx       # Contexto de layout
│   ├── useNotificationContext.jsx # Contexto de notificaciones
│   └── useShoppingContext.jsx     # Contexto de carrito
└── 📁 utils/                      # Utilidades generales
```

### Estructura de despliegue

```
📁 deployments/                    # Archivos de Docker
├── Dockerfile                     # Multi-stage build (dev/prod)
└── nginx.conf                     # Configuración de Nginx para producción
📄 docker-compose.yml              # Orchestración de contenedores
📄 .env.example                    # Template de variables de entorno
```

### Componentes destacados

Listado (no exhaustivo) de componentes visibles en `src/components`:

- `BackToTop.jsx`
- `GlightBox.jsx`
- `Jarallax.jsx`, `Parallax.jsx`
- `LogoBox.jsx`
- `PageBreadcrumb.jsx`, `PageTitle.jsx`
- `PasswordStrengthMeter.jsx`, `Preloader.jsx`
- `cards/ShowcaseCard.jsx`
- `footer/` — componentes `Footer1.jsx` ... `Footer8.jsx` y subcomponentes
- `form/` — `PasswordFormInput.jsx`, `SelectFormInput.jsx`, `TextAreaFormInput.jsx`, `TextFormInput.jsx`
- `topbar/` — `CartItem.jsx`, `FloatingSearch.jsx`, `MobileNavbarToggler.jsx`, `SearchInput.jsx`, `ShoppingCartOffcanvas.jsx`, `StickyHeader.jsx`, `ThemeToggleDropdown.jsx`, `TopNavigationBar.jsx`, `TopNavigationBarCustom.jsx`, `AppMenu/...`

Además hay hooks (`src/hooks`) y helpers que extienden la lógica de los componentes (por ejemplo, integraciones con BS-Stepper, control de scroll, manejo de viewport).

### Servicios y endpoints (API)

La comunicación con la API está centralizada en `src/services` usando Axios con configuración automática de headers y manejo de errores. La URL base se configura mediante `VITE_API_URL`.

#### Configuración del cliente HTTP

**Archivo:** `src/services/shared/http_client.js`

- **Base URL:** Configurada desde `VITE_API_URL`
- **Timeout:** 60 segundos
- **Autenticación:** Token JWT automático si existe en `sessionStorage`
- **Headers:** `Authorization: Bearer <token>` cuando aplica

#### Endpoints implementados

##### 1. Registro de usuarios
```http
POST /user/signup
```
**Archivo:** `src/services/users.js`  
**Propósito:** Registrar usuario con perfil de riesgo completo

**Payload:**
```json
{
  "email": "string",
  "fecha_nacimiento": "YYYY-MM-DD",
  "nivel_educativo_id": "number",
  "conocimiento_alt_inversion_id": "number",    // Pregunta 1
  "experiencia_invirtiendo_id": "number",       // Pregunta 2
  "porcentaje_ahorro_mensual_id": "number",     // Pregunta 3
  "porcentaje_ahorro_invertir_id": "number",    // Pregunta 4
  "tiempo_mantener_inversion_id": "number",     // Pregunta 5
  "busca_invertir_en_id": "number",             // Pregunta 6
  "proporcion_inversion_mantener_id": "number"  // Pregunta 7
}
```

##### 2. Crear sesión de asesoría
```http
POST /copilot/sessions
```
**Archivo:** `src/services/copilot_sessions.js`  
**Propósito:** Inicializar nueva sesión de chat con parámetros de inversión

**Payload:**
```json
{
  "proposito_sesion_id": "number",
  "objetivo_id": "number",
  "capital_inicial": "number",
  "horizonte_temporal": "number",
  "tolerancia_al_riesgo_id": "number"
}
```

##### 3. Enviar mensaje en sesión
```http
POST /copilot/sessions/:sesion_asesoria_id
```
**Archivo:** `src/services/copilot_sessions.js`  
**Propósito:** Enviar input del usuario y recibir respuesta del copilot

**Payload:**
```json
{
  "input": "string"
}
```

#### Manejo de errores

**Archivo:** `src/services/shared/errors.js`

- **`ApiError`** - Errores de respuesta del servidor
- **`ApiUnreachableError`** - Errores de red/conectividad  
- **`UnknownError`** - Errores no clasificados

La función `handleError()` mapea automáticamente errores de Axios a estas clases personalizadas.

### Variables de entorno importantes

- `VITE_API_URL` — URL base de la API (usada por Axios)
- `VITE_BASE_URL` — usada por `vite.config.js` para ajustar `base` del build (deploy path)

### Almacenamiento y autenticación

- **Token JWT:** Almacenado con clave `maverik-auth-token`
- **Storage:** `sessionStorage` (expira al cerrar pestaña/ventana)
- **Envío:** Automático via header `Authorization: Bearer <token>`
- **Gestión:** Centralizada en `src/services/shared/storage.js`

### Containerización con Docker

El proyecto incluye configuración completa de Docker con multi-stage builds:

#### Estructura de archivos
```
deployments/
├── Dockerfile         # Multi-stage: development, build, production
└── nginx.conf         # Configuración optimizada para SPA
docker-compose.yml     # Orchestración con perfiles
.env.example          # Template de variables
.dockerignore         # Optimización de contexto
```

#### Perfiles de Docker Compose
- **`dev`** - Desarrollo con hot reload (puerto 5173)
- **`prod`** - Producción con Nginx optimizado (puerto 80)  
- **`preview`** - Testing del build (puerto 4173)

#### Características de la imagen de producción
- ✅ **Multi-stage build** para optimizar tamaño
- ✅ **Nginx Alpine** como servidor web
- ✅ **Configuración SPA** para React Router
- ✅ **Cache headers** para assets estáticos
- ✅ **Compresión gzip** habilitada
- ✅ **Headers de seguridad** básicos

#### Comandos Docker esenciales
```bash
# Desarrollo
docker-compose --profile dev up --build

# Producción  
docker-compose --profile prod up --build

# Build manual
docker build -f deployments/Dockerfile --target production -t maverik-ui .
```

### Dependencias principales y su propósito

- React, React DOM — UI
- Vite — bundler / dev server
- Axios — cliente HTTP
- react-router-dom — ruteo
- bootstrap / react-bootstrap — estilos y componentes UI
- react-hook-form + yup — validación y manejo de formularios
- glightbox, isotope-layout, jarallax, swiper — efectos visuales, galerías y paralax
- react-toastify — notificaciones

### Consideraciones y recomendaciones para continuación del desarrollo

#### 🐳 1. Docker y containerización ✅ IMPLEMENTADO
- ✅ Proyecto dockerizado con multi-stage build
- ✅ Docker Compose para desarrollo local consistente
- 🔄 **Pendiente:** Configurar CI/CD para build automático de imágenes
- 🔄 **Pendiente:** Añadir health checks y optimización adicional

#### 🔐 2. Autenticación y tokens (ALTA PRIORIDAD)
- ⚠️ **Revisar:** `sessionStorage` vs `localStorage` para persistencia de sesión
- 🔄 **Implementar:** Interceptores de Axios para:
  - Adjuntar token automáticamente
  - Detectar 401 y manejar refresh token o redirect
- 🔄 **Considerar:** Sistema de refresh tokens para sesiones largas

#### 🚨 3. Manejo de errores y UX (ALTA PRIORIDAD)
- 🔄 **Mejorar:** Interceptores de Axios para mapeo centralizado de errores
- 🔄 **Implementar:** Feedback visual consistente para errores de API
- 🔄 **Añadir:** Logging y telemetría para debugging

#### 🔒 4. Seguridad y CORS
- 🔄 **Verificar:** Configuración CORS en backend
- 🔄 **Validar:** `VITE_API_URL` apunta a entornos correctos
- 🔄 **Implementar:** Medidas adicionales contra XSS

#### 📝 5. Tipado y pruebas (RECOMENDADO)
- 🔄 **Considerar:** Migración a TypeScript para mayor robustez
- 🔄 **Implementar:** Pruebas unitarias (Jest + React Testing Library)
- 🔄 **Añadir:** Tests de integración para servicios críticos

#### ⚡ 6. Rendimiento y experiencia
- 🔄 **Implementar:** Lazy loading para rutas pesadas
- 🔄 **Optimizar:** Imágenes (srcset/webp) en `assets/images/`
- 🔄 **Analizar:** Bundle size y code splitting

#### 🔧 7. Calidad del código y CI
- 🔄 **Configurar:** Pre-commit hooks (husky + lint-staged)
- 🔄 **Definir:** Pipeline CI completo (build, lint, tests)
- 🔄 **Automatizar:** Despliegue con `VITE_BASE_URL`

#### ♿ 8. UX y accesibilidad
- 🔄 **Evaluar:** Accesibilidad básica (a11y)
- 🔄 **Mejorar:** Focus management y keyboard navigation
- 🔄 **Validar:** Contrastes y labels

#### 📚 9. Documentación y on-boarding ✅ EN PROGRESO
- ✅ **Actualizada:** Documentación técnica completa
- ✅ **Creada:** Guía de Docker y deployment
- 🔄 **Pendiente:** `CONTRIBUTING.md` con convenciones
- 🔄 **Pendiente:** Documentación de API contracts

### Próximos pasos sugeridos (accionables)

#### Sprints inmediatos (Semana 1-2)

1. **🔐 Mejorar autenticación**
   ```bash
   # Implementar interceptores de Axios
   src/services/shared/http_client.js
   
   # Decidir estrategia de persistencia
   sessionStorage vs localStorage + refresh token
   ```

2. **⚙️ Configurar entorno**
   ```bash
   # Variables de entorno
   cp .env.example .env
   # VITE_API_URL=http://localhost:8000/api
   
   # Probar containerización
   docker-compose --profile dev up --build
   ```

#### Sprint medio plazo (Semana 3-4)

3. **🧪 Testing básico**
   ```bash
   # Instalar dependencias de testing
   npm install --save-dev @testing-library/react @testing-library/jest-dom vitest
   
   # Tests para servicios críticos
   src/services/__tests__/
   ```

4. **🚀 CI/CD inicial**
   ```bash
   # GitHub Actions básico
   .github/workflows/ci.yml
   
   # Docker registry setup
   docker build -t maverik-ui:latest .
   ```

#### Sprint largo plazo (Mes 2)

5. **📊 Monitoreo y analytics**
   - Error tracking (Sentry/LogRocket)
   - Performance monitoring
   - User analytics

6. **♿ Accesibilidad y UX**
   - Audit con herramientas automáticas
   - Focus management
   - Screen reader testing

---

### 📋 Checklist de integración con backend

#### Antes de conectar con API real:

- [ ] **Configurar CORS** en backend para dominios frontend
- [ ] **Validar contratos** de API (request/response schemas)
- [ ] **Documentar endpoints** faltantes (login, logout, profile, etc.)
- [ ] **Probar autenticación** end-to-end
- [ ] **Manejo de errores** consistente (códigos HTTP, mensajes)
- [ ] **Rate limiting** y timeouts apropiados
- [ ] **Environments** (dev/staging/prod) configurados

#### Variables de entorno por ambiente:

```bash
# Desarrollo local
VITE_API_URL=http://localhost:8000/api

# Staging
VITE_API_URL=https://api-staging.maverik.com/api

# Producción
VITE_API_URL=https://api.maverik.com/api
VITE_BASE_URL=/app  # Si se deploya en subdirectorio
```

---

## 📚 Referencias y documentación adicional

- **`README.md`** - Guía de inicio rápido y comandos básicos
- **`docs/docker.md`** - Documentación detallada de Docker y deployment
- **`package.json`** - Scripts disponibles y dependencias
- **`vite.config.js`** - Configuración de build y desarrollo
- **`jsconfig.json`** - Alias y configuración de VS Code

---

*Documento actualizado: 30 de septiembre de 2025*  
*Versión: 2.0 - Incluye containerización y restructuración*
