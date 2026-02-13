# 🚀 Moto Tracker - Backend API

API REST para el sistema de gestión de vehículos personales MotoTracker.

## 📋 Descripción

Backend desarrollado en **Java 17 + Spring Boot 3** que proporciona una API REST completa para:
- Gestión de vehículos (motos/carros)
- Registro de mantenimientos
- Control de gastos operativos
- Dashboard con estadísticas
- Autenticación JWT

## 🛠️ Stack Tecnológico

- **Java:** 17
- **Framework:** Spring Boot 3.2.x
- **Base de datos:** PostgreSQL 15+
- **Autenticación:** JWT (JSON Web Tokens)
- **ORM:** Spring Data JPA / Hibernate
- **Documentación:** Swagger/OpenAPI
- **Build:** Maven
- **Testing:** JUnit 5 + Mockito

## 📁 Estructura del Proyecto

```
src/
├── main/
│   ├── java/com/mototracker/
│   │   ├── MotoTrackerApplication.java
│   │   ├── config/              # Configuración (Security, CORS, JWT)
│   │   ├── controller/          # REST Controllers
│   │   ├── service/             # Lógica de negocio
│   │   ├── repository/          # Acceso a datos (JPA)
│   │   ├── entity/              # Entidades JPA
│   │   ├── dto/                 # Request/Response DTOs
│   │   ├── security/            # JWT, Filters, UserDetails
│   │   ├── exception/           # Exception handlers
│   │   └── util/                # Utilidades
│   └── resources/
│       ├── application.yml
│       ├── application-dev.yml
│       └── application-prod.yml
└── test/
    └── java/com/mototracker/    # Tests unitarios e integración
```

## 🚀 Quick Start

### Prerrequisitos

- Java 17+
- Maven 3.8+
- PostgreSQL 15+

### Instalación

```bash
# Clonar repositorio
git clone https://github.com/Andres-Gz/moto-tracker-backend.git
cd moto-tracker-backend

# Configurar base de datos
# Crear base de datos PostgreSQL: moto_tracker_dev

# Configurar variables de entorno (opcional)
export DB_HOST=localhost
export DB_PORT=5432
export DB_NAME=moto_tracker_dev
export DB_USER=postgres
export DB_PASSWORD=postgres
export JWT_SECRET=your-secret-key-change-in-production

# Compilar proyecto
mvn clean install

# Ejecutar aplicación
mvn spring-boot:run
```

### Configuración de Base de Datos

Editar `src/main/resources/application-dev.yml`:

```yaml
spring:
  datasource:
    url: jdbc:postgresql://localhost:5432/moto_tracker_dev
    username: postgres
    password: postgres
  jpa:
    hibernate:
      ddl-auto: update
    show-sql: true
```

## 📡 API Endpoints

La API estará disponible en: `http://localhost:8080/api`

### Documentación Swagger

Una vez iniciada la aplicación, acceder a:
- **Swagger UI:** http://localhost:8080/swagger-ui.html
- **OpenAPI JSON:** http://localhost:8080/v3/api-docs

### Endpoints Principales

#### Autenticación
- `POST /api/auth/register` - Registro de usuario
- `POST /api/auth/login` - Login
- `GET /api/auth/me` - Perfil de usuario

#### Vehículos
- `GET /api/vehicles` - Listar vehículos
- `POST /api/vehicles` - Crear vehículo
- `GET /api/vehicles/{id}` - Obtener vehículo
- `PUT /api/vehicles/{id}` - Actualizar vehículo
- `DELETE /api/vehicles/{id}` - Eliminar vehículo

#### Mantenimientos
- `GET /api/vehicles/{vehicleId}/maintenances` - Listar mantenimientos
- `POST /api/vehicles/{vehicleId}/maintenances` - Crear mantenimiento
- `PUT /api/vehicles/{vehicleId}/maintenances/{id}` - Actualizar
- `DELETE /api/vehicles/{vehicleId}/maintenances/{id}` - Eliminar

#### Gastos
- `GET /api/vehicles/{vehicleId}/expenses` - Listar gastos
- `POST /api/vehicles/{vehicleId}/expenses` - Crear gasto
- `PUT /api/vehicles/{vehicleId}/expenses/{id}` - Actualizar
- `DELETE /api/vehicles/{vehicleId}/expenses/{id}` - Eliminar

#### Dashboard
- `GET /api/dashboard` - Resumen general
- `GET /api/vehicles/{id}/stats` - Estadísticas de vehículo

## 🔐 Autenticación

La API utiliza JWT (JSON Web Tokens) para autenticación.

### Flujo de autenticación:

1. Login: `POST /api/auth/login`
2. Obtener token en respuesta
3. Incluir en headers: `Authorization: Bearer {token}`
4. Token expira en 24 horas

## 🧪 Testing

```bash
# Ejecutar todos los tests
mvn test

# Ejecutar tests con coverage
mvn test jacoco:report

# Ver reporte de coverage
open target/site/jacoco/index.html
```

## 🐳 Docker

```bash
# Construir imagen
docker build -t moto-tracker-backend .

# Ejecutar contenedor
docker run -p 8080:8080 \
  -e DB_HOST=host.docker.internal \
  -e DB_NAME=moto_tracker_dev \
  moto-tracker-backend
```

## 📊 Base de Datos

### Entidades principales:

- **Users** - Usuarios del sistema
- **Vehicles** - Vehículos registrados
- **Maintenances** - Mantenimientos realizados
- **Expenses** - Gastos operativos

Ver diagrama completo en: [moto-tracker-docs](https://github.com/Andres-Gz/moto-tracker-docs)

## 🔧 Variables de Entorno

| Variable | Descripción | Default |
|----------|-------------|---------|
| `DB_HOST` | Host de PostgreSQL | localhost |
| `DB_PORT` | Puerto de PostgreSQL | 5432 |
| `DB_NAME` | Nombre de la base de datos | moto_tracker_dev |
| `DB_USER` | Usuario de PostgreSQL | postgres |
| `DB_PASSWORD` | Password de PostgreSQL | postgres |
| `JWT_SECRET` | Secret key para JWT | (debe configurarse) |
| `JWT_EXPIRATION` | Tiempo de expiración del token (ms) | 86400000 (24h) |

## 📝 Convenciones de Código

- **Java Code Style:** Google Java Style Guide
- **Naming:**
  - Entities: PascalCase (User, Vehicle)
  - DTOs: Sufijo Request/Response (VehicleRequest, VehicleResponse)
  - Services: Sufijo Service (VehicleService)
  - Repositories: Sufijo Repository (VehicleRepository)
- **Commits:** Conventional Commits (feat:, fix:, docs:, etc.)

## 🚀 Deploy

### Producción

```bash
# Build JAR
mvn clean package -DskipTests

# Ejecutar JAR
java -jar target/moto-tracker-backend-1.0.0.jar \
  --spring.profiles.active=prod
```

## 📚 Documentación Adicional

- [Documentación completa del proyecto](https://github.com/Andres-Gz/moto-tracker-docs)
- [Especificación de API](https://github.com/Andres-Gz/moto-tracker-docs/blob/main/docs/04-api-specification.md)
- [Diseño de Base de Datos](https://github.com/Andres-Gz/moto-tracker-docs/blob/main/docs/02-database-design.md)

## 🤝 Contribución

1. Fork el proyecto
2. Crear feature branch (`git checkout -b feature/nueva-funcionalidad`)
3. Commit cambios (`git commit -m 'feat: agregar nueva funcionalidad'`)
4. Push al branch (`git push origin feature/nueva-funcionalidad`)
5. Crear Pull Request

## 📄 Licencia

MIT License - ver [LICENSE](LICENSE) para más detalles

## 👨‍💻 Autor

**Andre García**
- GitHub: [@Andres-Gz](https://github.com/Andres-Gz)

---

⭐ Si te gusta el proyecto, dale una estrella en GitHub!
