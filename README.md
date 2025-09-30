# Proyecto Maverik: Interfaz de Usuario

Este proyecto es una aplicación frontend basada en React y configurada con Vite para una experiencia de desarrollo rápida y optimizada. Incluye una variedad de dependencias y configuraciones para proporcionar una funcionalidad avanzada y una interfaz atractiva.

## 🚀 Inicio rápido

### Método 1: Docker (Recomendado)

La forma más rápida de ejecutar el proyecto es usando Docker:

1. **Clona el repositorio:**
   ```bash
   git clone https://github.com/alexcabezas1/maverik-react-js.git
   cd maverik-react-js
   ```

2. **Configura las variables de entorno:**
   ```bash
   cp .env.example .env
   # Edita .env con la URL de tu API
   ```

3. **Ejecuta con Docker:**
   ```bash
   # Para desarrollo (con hot reload)
   docker-compose --profile dev up --build
   
   # Para producción
   docker-compose --profile prod up --build
   ```

4. **Accede a la aplicación:**
   - Desarrollo: `http://localhost:5173`
   - Producción: `http://localhost:80`

### Método 2: Instalación local

1. **Clona el repositorio:**
   ```bash
   git clone https://github.com/fliquinuade/maverik-react.git
   cd maverik-react
   ```

2. **Instala las dependencias:**
   ```bash
   npm install
   ```

3. **Configura variables de entorno:**
   ```bash
   cp .env.example .env
   # Edita .env con tus configuraciones
   ```

4. **Inicia el servidor de desarrollo:**
   ```bash
   npm run dev
   ```

5. **Accede a la aplicación:**
   ```
   http://localhost:5173
   ```

## 📁 Estructura del proyecto

```
maverik_react/
├── src/                    # Código fuente
│   ├── components/         # Componentes reutilizables
│   ├── pages/             # Páginas de la aplicación
│   ├── layouts/           # Layouts (Default, Auth, Blog, Shop)
│   ├── services/          # Cliente HTTP y servicios API
│   ├── hooks/             # Hooks personalizados
│   ├── states/            # Contextos y estados globales
│   ├── utils/             # Utilidades generales
│   └── assets/            # Recursos estáticos
├── deployments/           # Archivos de Docker
│   ├── Dockerfile         # Configuración multi-stage
│   └── nginx.conf         # Configuración de Nginx
├── docs/                  # Documentación
├── public/                # Archivos públicos
├── docker-compose.yml     # Orchestración de contenedores
└── package.json           # Dependencias y scripts
```

## 🐳 Docker

El proyecto está completamente dockerizado con soporte para desarrollo y producción:

### Perfiles disponibles:

- **`dev`**: Desarrollo con hot reload (puerto 5173)
- **`prod`**: Producción con Nginx optimizado (puerto 80)
- **`preview`**: Testing del build (puerto 4173)

### Comandos Docker:

```bash
# Desarrollo
docker-compose --profile dev up --build

# Producción
docker-compose --profile prod up --build

# Preview/Testing
docker-compose --profile preview up --build

# Detener servicios
docker-compose down
```

### Variables de entorno:

Crea un archivo `.env` basado en `.env.example`:

```bash
VITE_API_URL=http://localhost:8000/api
VITE_BASE_URL=
```

## ⚙️ Scripts disponibles

```bash
npm run dev      # Servidor de desarrollo
npm run build    # Build para producción
npm run preview  # Preview del build
npm run lint     # Ejecutar ESLint
npm run format   # Formatear código con Prettier
```

## 🛠️ Tecnologías principales

- **React 18** - Biblioteca de UI
- **Vite** - Build tool y dev server
- **Bootstrap 5** - Framework CSS
- **React Router DOM** - Enrutamiento
- **Axios** - Cliente HTTP
- **React Hook Form + Yup** - Formularios y validación
- **React Bootstrap** - Componentes UI
- **SCSS** - Preprocesador CSS
- **Docker** - Containerización

## 📊 Funcionalidades principales

- ✅ **Registro de usuarios** con formulario multi-paso
- ✅ **Sistema de asesoría** con chat interactivo
- ✅ **Autenticación** con tokens JWT
- ✅ **Interfaz responsive** con Bootstrap
- ✅ **Temas dinámicos** (claro/oscuro)
- ✅ **Galería de imágenes** con efectos visuales
- ✅ **Carrito de compras** funcional
- ✅ **Múltiples layouts** (Default, Auth, Blog, Shop)

## 🔧 Configuración

### Variables de entorno requeridas:

```bash
VITE_API_URL=http://localhost:8000/api  # URL de la API backend
VITE_BASE_URL=                          # Base path (opcional)
```

### Archivos de configuración:

- **vite.config.js** - Configuración de Vite y alias
- **jsconfig.json** - Alias para VS Code
- **package.json** - Dependencias y scripts
- **.eslintrc.cjs** - Reglas de ESLint
- **.prettierrc** - Formato de código

## 🚢 Deployment

### Con Docker (Recomendado):

```bash
# Build imagen de producción
docker build -f deployments/Dockerfile --target production -t maverik-ui .

# Ejecutar contenedor
docker run -p 80:80 maverik-ui
```

### Build tradicional:

```bash
npm run build
npm run preview
```

Los archivos optimizados se generan en la carpeta `dist/`.

## 📚 Documentación

- **`docs/PROYECTO_MAVERIK_FRONTEND.md`** - Documentación técnica completa
- **`docs/docker.md`** - Guía detallada de Docker

## 📄 Licencia

Este proyecto es privado y pertenece a Maverik.

---
⏰ Última actualización: 30 de septiembre de 2025
