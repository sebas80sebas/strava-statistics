# Statistics for Strava

[English](#english) | [Español](#español)

---

## Español

### Descripción

Esta es una instancia personalizada de **Statistics for Strava**, una herramienta que te permite analizar y visualizar tus estadísticas de actividades deportivas desde Strava. Incluye dashboards personalizados, mapas de calor, análisis de rendimiento y más.

### Inicio Rápido

#### Requisitos Previos

- Docker y Docker Compose instalados
- Una cuenta de Strava
- Credenciales de API de Strava (Client ID y Client Secret)

#### Configuración

1. **Clona el repositorio:**
   ```bash
   git clone <tu-repositorio>
   cd statistics-for-strava
   ```

2. **Crea los archivos de configuración:**
   ```bash
   cp .env.example .env
   cp config/config.yaml.example config/config.yaml
   ```

3. **Configura tus credenciales en `.env`:**
   ```env
   STRAVA_CLIENT_ID=tu_client_id_aqui
   STRAVA_CLIENT_SECRET=tu_client_secret_aqui
   STRAVA_REFRESH_TOKEN=se_obtiene_automaticamente
   TZ=Europe/Madrid
   ```

4. **Personaliza la configuración en `config/config.yaml`:**
   - Añade tu fecha de nacimiento
   - Configura tus zonas de frecuencia cardíaca
   - Establece tu historial de peso
   - Personaliza el aspecto y los widgets del dashboard

5. **Inicia los contenedores:**
   ```bash
   docker-compose up -d
   ```

6. **Accede a la aplicación:**
   - Abre `http://localhost:8080` en tu navegador
   - La aplicación te guiará a través del flujo de autenticación de Strava
   - Obtén tu token de refresco y añádelo a `.env`

### Estructura del Proyecto

```
.
├── config/
│   └── app/
│       └── config.yaml          # Configuración principal personalizada
├── storage/
│   ├── database/                # Base de datos (generada automáticamente)
│   └── files/                   # Archivos almacenados
├── build/                        # Construcción de la aplicación (generada)
├── docker-compose.yml           # Configuración de contenedores
├── .env                         # Variables de entorno (NO SUBIR A GIT)
└── .gitignore                   # Archivos a ignorar en Git
```

### Configuración Avanzada

#### Variables de Entorno (`.env`)

| Variable | Descripción | Requerido |
|----------|-------------|----------|
| `STRAVA_CLIENT_ID` | ID de cliente de Strava | Sí |
| `STRAVA_CLIENT_SECRET` | Secreto de cliente de Strava | Sí |
| `STRAVA_REFRESH_TOKEN` | Token de refresco (obtenido tras autenticación) | Sí |
| `TZ` | Zona horaria | No |
| `PROXY_HOST` | Dominio personalizado | No |
| `PROXY_PORT` | Puerto de la aplicación | No |

#### Daemon (Tareas Automáticas)

El contenedor `daemon` ejecuta tareas programadas. Configúralas en `config.yaml`:

```yaml
daemon:
  cron:
    - action: 'importDataAndBuildApp'
      expression: '0 14 * * *'      # Diario a las 14:00
      enabled: true
```

### Documentación

Para información detallada sobre la configuración:
- [Documentación oficial](https://statistics-for-strava-docs.robiningelbrecht.be)
- [Guía de instalación](https://statistics-for-strava-docs.robiningelbrecht.be/#/getting-started/installation)
- [Configuración de AI](https://statistics-for-strava-docs.robiningelbrecht.be/#/configuration/ai-integration)

### Seguridad

IMPORTANTE: Nunca subas a GitHub:
- `.env` (contiene tus credenciales)
- `/storage/database/` (datos personales)
- `/build/` (archivos generados)

El archivo `.gitignore` está configurado para proteger estos archivos automáticamente.

### Docker Compose

El proyecto incluye dos servicios:

- **app**: Servidor web principal (puerto 8080)
- **daemon**: Gestor de tareas automáticas (opcional)

Para usar solo la aplicación sin el daemon:
```bash
docker-compose up -d app
```

### Contribuciones

Las contribuciones son bienvenidas. Por favor, abre un issue o pull request.

### Licencia

Este proyecto utiliza la configuración de [Statistics for Strava](https://github.com/robiningelbrecht/strava-statistics).

---

## English

### Description

This is a custom instance of **Statistics for Strava**, a tool that allows you to analyze and visualize your sports activity statistics from Strava. It includes personalized dashboards, heatmaps, performance analytics, and more.

### Quick Start

#### Prerequisites

- Docker and Docker Compose installed
- A Strava account
- Strava API credentials (Client ID and Client Secret)

#### Setup

1. **Clone the repository:**
   ```bash
   git clone <your-repository>
   cd statistics-for-strava
   ```

2. **Create configuration files:**
   ```bash
   cp .env.example .env
   cp config/config.yaml.example config/config.yaml
   ```

3. **Set your credentials in `.env`:**
   ```env
   STRAVA_CLIENT_ID=your_client_id_here
   STRAVA_CLIENT_SECRET=your_client_secret_here
   STRAVA_REFRESH_TOKEN=obtained_automatically
   TZ=Europe/Madrid
   ```

4. **Personalize configuration in `config/config.yaml`:**
   - Add your date of birth
   - Configure your heart rate zones
   - Set your weight history
   - Customize dashboard appearance and widgets

5. **Start the containers:**
   ```bash
   docker-compose up -d
   ```

6. **Access the application:**
   - Open `http://localhost:8080` in your browser
   - The app will guide you through Strava authentication flow
   - Obtain your refresh token and add it to `.env`

### Project Structure

```
.
├── config/
│   └── app/
│       └── config.yaml          # Main custom configuration
├── storage/
│   ├── database/                # Database (auto-generated)
│   └── files/                   # Stored files
├── build/                        # Application build (generated)
├── docker-compose.yml           # Container configuration
├── .env                         # Environment variables (DO NOT COMMIT)
└── .gitignore                   # Git ignore rules
```

### Advanced Configuration

#### Environment Variables (`.env`)

| Variable | Description | Required |
|----------|-------------|----------|
| `STRAVA_CLIENT_ID` | Strava client ID | Yes |
| `STRAVA_CLIENT_SECRET` | Strava client secret | Yes |
| `STRAVA_REFRESH_TOKEN` | Refresh token (obtained after auth) | Yes |
| `TZ` | Timezone | No |
| `PROXY_HOST` | Custom domain | No |
| `PROXY_PORT` | Application port | No |

#### Daemon (Scheduled Tasks)

The `daemon` container runs scheduled tasks. Configure them in `config.yaml`:

```yaml
daemon:
  cron:
    - action: 'importDataAndBuildApp'
      expression: '0 14 * * *'      # Daily at 14:00
      enabled: true
```

### Documentation

For detailed configuration information:
- [Official Documentation](https://statistics-for-strava-docs.robiningelbrecht.be)
- [Installation Guide](https://statistics-for-strava-docs.robiningelbrecht.be/#/getting-started/installation)
- [AI Integration](https://statistics-for-strava-docs.robiningelbrecht.be/#/configuration/ai-integration)

### Security

IMPORTANT: Never commit to GitHub:
- `.env` (contains your credentials)
- `/storage/database/` (personal data)
- `/build/` (generated files)

The `.gitignore` file is configured to protect these files automatically.

### Docker Compose

The project includes two services:

- **app**: Main web server (port 8080)
- **daemon**: Automated task manager (optional)

To run only the app without the daemon:
```bash
docker-compose up -d app
```

### Contributing

Contributions are welcome. Please open an issue or pull request.

### License

This project uses the configuration from [Statistics for Strava](https://github.com/robiningelbrecht/strava-statistics).