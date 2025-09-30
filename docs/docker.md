# Docker para Maverik UI

Este documento explica cómo usar Docker para desarrollar y desplegar la aplicación frontend de Maverik.

## Archivos Docker

- `deployments/Dockerfile` - Configuración multi-stage para desarrollo y producción
- `docker-compose.yml` - Orchestración de servicios con diferentes perfiles
- `deployments/nginx.conf` - Configuración de Nginx para producción
- `.dockerignore` - Archivos excluidos del contexto de build
- `.env.example` - Template de variables de entorno

## Comandos rápidos

### Desarrollo

```bash
# Crear archivo de variables de entorno
cp .env.example .env

# Editar .env con tus valores
# VITE_API_URL=http://localhost:8000/api

# Ejecutar en modo desarrollo
docker-compose --profile dev up --build

# La aplicación estará disponible en http://localhost:5173
```

### Producción

```bash
# Construir y ejecutar en modo producción
docker-compose --profile prod up --build

# La aplicación estará disponible en http://localhost:80
```

### Preview (testing del build)

```bash
# Construir y preview
docker-compose --profile preview up --build

# La aplicación estará disponible en http://localhost:4173
```

## Variables de entorno

Las siguientes variables pueden configurarse en el archivo `.env`:

- `VITE_API_URL` - URL base de la API backend (ej: `http://localhost:8000/api`)
- `VITE_BASE_URL` - Base path para deployment (dejar vacío para root)

## Comandos Docker individuales

### Desarrollo

```bash
# Build imagen de desarrollo
docker build -f deployments/Dockerfile --target development -t maverik-ui:dev .

# Ejecutar contenedor de desarrollo
docker run -p 5173:5173 -v $(pwd):/app -v /app/node_modules maverik-ui:dev
```

### Producción

```bash
# Build imagen de producción
docker build -f deployments/Dockerfile --target production -t maverik-ui:prod .

# Ejecutar contenedor de producción
docker run -p 80:80 maverik-ui:prod
```

## Características del setup

### Dockerfile Multi-stage

1. **Etapa de build**: Instala dependencias y construye la aplicación
2. **Etapa de producción**: Usa Nginx para servir archivos estáticos
3. **Etapa de desarrollo**: Configurada para hot reload y desarrollo

### Nginx

- Configurado como SPA (Single Page Application)
- Cache headers para assets estáticos
- Compresión gzip habilitada
- Headers de seguridad básicos

### Docker Compose

- **Perfil `dev`**: Para desarrollo con hot reload
- **Perfil `prod`**: Para producción con Nginx
- **Perfil `preview`**: Para testing del build

## Optimizaciones

- Multi-stage build reduce el tamaño final de la imagen
- `.dockerignore` excluye archivos innecesarios
- Cache de layers de Docker para builds más rápidos
- Volumes en desarrollo para hot reload

## Troubleshooting

### El contenedor no inicia

```bash
# Ver logs
docker-compose --profile dev logs -f

# Verificar que los puertos no estén en uso
netstat -an | grep :5173
```

### Variables de entorno no se cargan

- Verificar que el archivo `.env` existe
- Confirmar que las variables empiezan con `VITE_`
- Reconstruir la imagen después de cambiar variables

### Problemas de permisos (Linux/Mac)

```bash
# Si hay problemas con node_modules en desarrollo
docker-compose --profile dev down -v
docker-compose --profile dev up --build
```

## Deployment

Para deployment en producción:

1. Configurar variables de entorno correctas en `.env`
2. Usar el perfil de producción: `docker-compose --profile prod up -d`
3. Configurar proxy reverso si es necesario
4. Considerar usar registry de Docker para distribución

