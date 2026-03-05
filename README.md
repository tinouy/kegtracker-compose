# KegTracker Docker Compose

Configuraciones Docker Compose para diferentes entornos de KegTracker.

## 🚀 Versiones Disponibles

### 📁 Archivos de Configuración

| Archivo | Versión | Descripción | Uso |
|---------|---------|-------------|-----|
| `docker-compose.yml` | Demo (actual) | Versión demo con datos pre-cargados | Desarrollo y demos |
| `docker-compose.demo.yml` | Demo | Versión demo específica | Demos organizados |
| `docker-compose.prod.yml` | 0.1.0 | Versión de producción limpia | Producción |

## 🎯 Demo (Datos Pre-cargados)

### Ejecución Rápida
```bash
# Usando configuración actual
docker-compose up -d

# O usando configuración específica demo
docker-compose -f docker-compose.demo.yml up -d
```

### ✅ Características Demo
- **Backend**: `tinouy/kegtracker-backend:demo`
- **Frontend**: `tinouy/kegtracker-frontend:demo`
- **Base de datos**: Pre-inicializada con datos demo
- **Usuarios**: 7 usuarios demo (admin@demo.com, etc.)
- **Contraseña**: `demo123` para todos
- **Puerto Backend**: 8000
- **Puerto Frontend**: 8080

### 🏭 Datos Demo Incluidos
- **2 Cervecerías**: Norte y Sur
- **7 Usuarios**: Con diferentes roles
- **6 Barriles**: En diferentes estados
- **Listo para usar**: Sin configuración adicional

## 🏭 Producción 0.1.0 (Limpia)

### Ejecución
```bash
# Copiar variables de entorno
cp .env.example .env
# Editar .env con tus valores

# Ejecutar versión producción
docker-compose -f docker-compose.prod.yml up -d
```

### ✅ Características Producción
- **Backend**: `tinouy/kegtracker-backend:0.1.0`
- **Frontend**: `tinouy/kegtracker-frontend:0.1.0`
- **Base de datos**: Vacía (requiere inicialización)
- **Volúmenes**: Persistencia de datos
- **Health checks**: Monitoreo de salud
- **Variables de entorno**: Configurables

### 🔧 Configuración Requerida

Crear archivo `.env`:
```bash
# Backend
BACKEND_HOST=kegtracker-backend
BACKEND_PORT=8000

# Frontend  
FRONTEND_HOST=kegtracker-frontend
FRONTEND_PORT=80
FRONTEND_FQDN=https://tu-dominio.com

# Base de datos
DB_ENGINE=sqlite
DB_URL=sqlite:///./data/kegtracker.db

# Email (SMTP)
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=tu-email@gmail.com
SMTP_PASS=tu-password
SMTP_FROM=no-reply@tu-dominio.com

# Seguridad
SECRET_KEY=tu-clave-secreta-muy-segura

# Zona horaria
TZ=America/Montevideo
```

## 🛠️ Comandos Útiles

### Gestión de Servicios
```bash
# Ver logs
docker-compose logs -f backend
docker-compose logs -f frontend

# Reiniciar servicios
docker-compose restart backend
docker-compose restart frontend

# Parar servicios
docker-compose down

# Parar y eliminar volúmenes
docker-compose down -v
```

### Mantenimiento
```bash
# Actualizar imágenes
docker-compose pull

# Rebuild completo
docker-compose down
docker-compose up -d --build

# Ver estado de servicios
docker-compose ps
```

## 🔄 Migración Entre Versiones

### De Demo a Producción
```bash
# 1. Parar demo
docker-compose down

# 2. Configurar variables
cp .env.example .env
# Editar .env

# 3. Iniciar producción
docker-compose -f docker-compose.prod.yml up -d

# 4. Inicializar via web
# Ir a http://localhost:8080 y usar el wizard
```

### De Producción a Demo (Testing)
```bash
# 1. Backup de datos (si necesario)
docker cp kegtracker-backend-prod:/app/data/kegtracker.db ./backup.db

# 2. Parar producción
docker-compose -f docker-compose.prod.yml down

# 3. Iniciar demo
docker-compose -f docker-compose.demo.yml up -d
```

## 🌐 Acceso

### Direcciones por Defecto
- **Frontend**: http://localhost:8080
- **Backend API**: http://localhost:8000
- **Documentación API**: http://localhost:8000/docs

### Usuarios Demo (solo versión demo)
```
admin@demo.com      | Global Admin | demo123
norte@demo.com      | Admin        | demo123  
sur@demo.com        | Admin        | demo123
modnorte@demo.com   | Moderator    | demo123
modsur@demo.com     | Moderator    | demo123
usernorte@demo.com  | User         | demo123
usersur@demo.com    | User         | demo123
```

## 📊 Monitoreo

### Health Checks (Solo Producción)
```bash
# Ver estado de salud
docker inspect kegtracker-backend-prod | grep Health -A 10

# Logs de health check
docker logs kegtracker-backend-prod | grep health
```

### Métricas
```bash
# Uso de recursos
docker stats kegtracker-backend-prod kegtracker-frontend-prod

# Espacio en disco (volúmenes)
docker system df
```

## 🐛 Troubleshooting

### Problemas Comunes
```bash
# Error de conexión backend-frontend
docker-compose logs backend

# Problema de permisos
sudo chown -R 1000:1000 ./data

# Puerto ocupado
sudo lsof -i :8000
sudo lsof -i :8080

# Limpiar todo
docker-compose down -v
docker system prune -f
```

## 📄 Licencia

[MIT License](../LICENSE) 