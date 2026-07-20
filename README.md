# 🚀 FinFlow Loan Management System

A **production-grade microservices-based backend system** built using Spring Boot, Spring Cloud, Docker, RabbitMQ, and comprehensive monitoring tools like **Prometheus & Grafana** to digitalize the complete loan lifecycle — from application to approval and notification.

[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.5.12-brightgreen.svg)](https://spring.io/projects/spring-boot)
[![Java](https://img.shields.io/badge/Java-21-orange.svg)](https://www.oracle.com/java/)
[![Docker](https://img.shields.io/badge/Docker-Compose-blue.svg)](https://www.docker.com/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

---

## 🧠 Overview

FinFlow simulates a **real-world banking loan processing system** with enterprise-grade features:

* 🔐 **Secure Authentication** - JWT-based authentication with role-based access control
* 📝 **Applicant Workflows** - Complete loan application lifecycle management
* ✅ **Admin Verification** - Multi-stage approval workflow with document validation
* 📁 **Document Management** - Secure file upload and storage system
* 🔔 **Event-Driven Notifications** - Real-time notifications using RabbitMQ
* 🌐 **API Gateway** - Centralized routing with security filters
* 📊 **Real-time Monitoring** - Prometheus metrics with Grafana dashboards
* 🔍 **Distributed Tracing** - End-to-end request tracing with Zipkin

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                   Client Layer                               │
│          (Postman / Swagger UI / Frontend)                   │
└──────────────────────┬──────────────────────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────────────────────┐
│              API Gateway (Port 8080)                         │
│         JWT Authentication + Request Routing                 │
└──────────────────────┬──────────────────────────────────────┘
                       │
       ┌───────────────┼───────────────┐
       │               │               │
       ▼               ▼               ▼
┌──────────────┐ ┌──────────────┐ ┌──────────────┐
│Auth Service  │ │Application   │ │Document      │
│  (8081)      │ │Service       │ │Service       │
│              │ │  (8082)      │ │  (8083)      │
└──────┬───────┘ └──────┬───────┘ └──────┬───────┘
       │               │               │
       ▼               ▼               ▼
┌──────────────┐ ┌──────────────┐ ┌──────────────┐
│Admin Service │ │Notification  │ │Config Server │
│  (8084)      │ │Service       │ │  (8888)      │
│              │ │  (8085)      │ │              │
└──────┬───────┘ └──────┬───────┘ └──────────────┘
       │               │
       │      ┌────────┴────────┐
       │      │                 │
       ▼      ▼                 ▼
┌──────────────────┐    ┌──────────────────┐
│   MySQL (3307)   │    │ RabbitMQ (5672)  │
│  Multiple DBs    │    │  Management UI   │
└──────────────────┘    │    (15672)       │
                        └──────────────────┘
       │
       └──────────────┬──────────────┐
                      │              │
                      ▼              ▼
         ┌──────────────────┐ ┌──────────────────┐
         │Eureka Server     │ │Zipkin (9411)     │
         │Service Discovery │ │Distributed       │
         │     (8761)       │ │Tracing           │
         └──────────────────┘ └──────────────────┘
                      │
         ┌────────────┴────────────┐
         ▼                         ▼
┌──────────────────┐      ┌──────────────────┐
│Prometheus (9090) │      │Grafana (3000)    │
│Metrics Collection│◄─────┤Visualization     │
└──────────────────┘      └──────────────────┘
```

---

## 🔧 Tech Stack

### Backend Framework
* **Java 21** - Latest LTS version with enhanced performance
* **Spring Boot 3.5.12** - Modern, production-ready framework
* **Spring Security** - JWT-based authentication & authorization
* **Spring Cloud Gateway** - Reactive API gateway with routing
* **Spring Data JPA** - Hibernate ORM for database operations

### Microservices Architecture
* **Eureka Server** - Service discovery and registration
* **Spring Cloud Config** - Centralized configuration management
* **OpenFeign** - Declarative REST client for inter-service communication
* **RabbitMQ** - Event-driven asynchronous messaging
* **Docker & Docker Compose** - Containerization and orchestration

### Monitoring & Observability
* **Prometheus** - Time-series metrics collection and storage
* **Grafana** - Real-time metrics visualization and dashboards
* **Zipkin** - Distributed tracing and request tracking
* **Spring Boot Actuator** - Production-ready features and health checks
* **Micrometer** - Application metrics facade

### Database & Storage
* **MySQL 8.4** - Reliable relational database with multiple schemas
* **File System Storage** - Document upload and management

### API Documentation
* **Swagger/OpenAPI 3.0** - Interactive API documentation and testing

### Development Tools
* **Maven 3.9.9** - Dependency management and build automation
* **Git** - Version control
* **SonarQube Integration** - Code quality and security analysis

---

## 📦 Microservices

| Service              | Port  | Description                                    | Key Features                          |
| -------------------- | ----- | ---------------------------------------------- | ------------------------------------- |
| **API Gateway**      | 8080  | Central entry point with security & routing    | JWT validation, Load balancing        |
| **Auth Service**     | 8081  | User authentication & JWT generation           | Signup, Login, User management        |
| **Application Service** | 8082 | Loan application lifecycle management       | CRUD operations, Status tracking      |
| **Document Service** | 8083  | Upload & manage loan documents                 | File upload, Document verification    |
| **Admin Service**    | 8084  | Approval workflow & orchestration              | Review, Approve/Reject applications   |
| **Notification Service** | 8085 | Async notifications via RabbitMQ          | Event consumption, Notification store |
| **Eureka Server**    | 8761  | Service registry & discovery                   | Health checks, Load balancing         |
| **Config Server**    | 8888  | Centralized configuration management           | Git-based config, Dynamic refresh     |

### Supporting Infrastructure

| Component            | Port  | Description                                    |
| -------------------- | ----- | ---------------------------------------------- |
| **MySQL**            | 3307  | Database with 5 separate schemas               |
| **RabbitMQ**         | 5672  | Message broker for async communication         |
| **RabbitMQ UI**      | 15672 | Management dashboard (guest/guest)             |
| **Zipkin**           | 9411  | Distributed tracing system                     |
| **Prometheus**       | 9090  | Metrics collection and storage                 |
| **Grafana**          | 3000  | Metrics visualization (admin/admin)            |

---

## 🔄 Workflow

### 👤 Applicant Flow

```
1. Sign Up → Create new user account
2. Login → Receive JWT token
3. Create Application → Initialize loan request (DRAFT status)
4. Upload Documents → Attach required documents
   - Identity proof
   - Income proof
   - Address proof
5. Submit Application → Change status to PENDING
6. Track Status → Monitor application progress
7. View Notifications → Get updates on application status
```

**Application States:** `DRAFT` → `PENDING` → `UNDER_REVIEW` → `APPROVED/REJECTED`

---

### 🧑‍💼 Admin Flow

```
1. Login → Authenticate as admin
2. View Queue → See all pending applications
3. Review Application → Check applicant details
4. Verify Documents → Validate uploaded documents
5. Make Decision → Approve or Reject with comments
6. Auto-Notification → System publishes event to RabbitMQ
```

**Admin Actions:**
- View all applications with filters
- Update application status
- Add review comments
- Approve/Reject applications

---

### 🔔 Notification System (Event-Driven)

```
Admin Action (Approve/Reject)
         ↓
Publish Event to RabbitMQ Queue
         ↓
Notification Service Consumes Event
         ↓
Store Notification in Database
         ↓
User Fetches via GET /notifications API
```

**Event Types:**
- `APPLICATION_APPROVED`
- `APPLICATION_REJECTED`
- `DOCUMENTS_VERIFIED`
- `UNDER_REVIEW`

---

## 🔐 Security

### Authentication & Authorization
* **JWT (JSON Web Token)** based stateless authentication
* **BCrypt password encoding** for secure password storage
* **Role-Based Access Control (RBAC)** with two roles:
  - `APPLICANT` - Can create and manage their own applications
  - `ADMIN` - Can view, review, and approve/reject all applications

### Security Features
* ✅ Password encryption using BCrypt
* ✅ JWT token expiration (configurable, default: 1 hour)
* ✅ Secure HTTP headers via Spring Security
* ✅ CORS configuration for cross-origin requests
* ✅ API Gateway level authentication filter
* ✅ Service-to-service communication security

### Default Admin Account
The system automatically seeds an admin account on first startup:
- **Email:** `admin@finflow.com`
- **Password:** `admin123`
- **Role:** `ADMIN`

⚠️ **Security Note:** Change the default admin password immediately in production!

---

## 📊 Monitoring & Observability

### 🔹 Spring Boot Actuator
Each microservice exposes health and metrics endpoints:

```bash
# Health check
http://localhost:{port}/actuator/health

# Prometheus metrics
http://localhost:{port}/actuator/prometheus

# All actuator endpoints
http://localhost:{port}/actuator
```

**Available Metrics:**
- Application health status
- JVM memory usage
- Garbage collection statistics
- HTTP request metrics
- Database connection pool stats
- Custom business metrics

---

### 🔹 Prometheus
Scrapes metrics from all services at 5-second intervals:

```bash
# Prometheus UI
http://localhost:9090

# View targets
http://localhost:9090/targets

# Run queries
http://localhost:9090/graph
```

**Monitored Services:**
- All 6 microservices (auth, application, document, admin, notification, gateway)
- Real-time metric collection
- Historical data retention
- Alert rule configuration support

---

### 🔹 Grafana
Pre-configured to visualize Prometheus metrics:

```bash
# Grafana Dashboard
http://localhost:3000

# Default Credentials
Username: admin
Password: admin
```

**Dashboard Metrics:**
- 📈 Request count and rate
- ⏱️ Average response time
- ❌ Error rate and 5xx responses
- 💾 JVM memory usage (heap/non-heap)
- 🔄 CPU usage per service
- 🗄️ Database query performance
- 🌐 Active HTTP connections

**Create Custom Dashboards:**
1. Login to Grafana
2. Add Prometheus as data source (`http://prometheus:9090`)
3. Import pre-built dashboards or create custom ones
4. Set up alerts for critical metrics

---

### 🔹 Zipkin (Distributed Tracing)
Tracks requests across microservices:

```bash
# Zipkin UI
http://localhost:9411

# View traces
http://localhost:9411/zipkin/
```

**Tracing Features:**
- End-to-end request flow visualization
- Service dependency mapping
- Latency analysis per service
- Error identification in distributed calls

---

### 📊 Monitoring Flow

```
Microservice → Actuator → Prometheus → Grafana Dashboard
                              ↓
                         Alert Manager (optional)
```

---

## 🐳 Docker Setup & Deployment

### Prerequisites
- Docker Desktop or Docker Engine (20.10+)
- Docker Compose (v2.0+)
- 8GB RAM minimum (16GB recommended)
- Ports 3000, 3307, 5672, 8080-8085, 8761, 8888, 9090, 9411, 15672 available

---

### 🔹 Quick Start (Development)

#### Option 1: Using Docker Compose (Recommended)

```bash
# Clone the repository
git clone https://github.com/maheshsingh20/Loan-Management-System.git
cd Loan-Management-System

# Start all services
docker-compose up --build

# Run in detached mode
docker-compose up --build -d

# View logs
docker-compose logs -f

# Stop all services
docker-compose down

# Stop and remove volumes (clean slate)
docker-compose down -v
```

#### Option 2: Manual Build (if you have Maven installed)

```bash
# Build all services
mvn clean package -DskipTests

# Then run with docker-compose
docker-compose up
```

---

### 🔹 Service Startup Order

The system starts in the following order (managed by Docker Compose):

1. **Infrastructure** (MySQL, RabbitMQ, Zipkin) - Wait for health checks
2. **Config Server** - Centralized configuration
3. **Eureka Server** - Service discovery
4. **Core Services** (Auth, Application, Document, Admin, Notification)
5. **API Gateway** - Entry point (depends on all services)
6. **Monitoring** (Prometheus, Grafana)

**Note:** First startup takes 5-10 minutes to pull images and build services.

---

### 🔹 Health Checks

Wait for all services to be healthy before testing:

```bash
# Check service health
curl http://localhost:8080/actuator/health  # API Gateway
curl http://localhost:8081/actuator/health  # Auth Service
curl http://localhost:8082/actuator/health  # Application Service

# View Eureka dashboard to see registered services
http://localhost:8761
```

---

### 🔹 Database Initialization

MySQL automatically creates 5 databases on first startup:
- `auth_db` - User credentials and profiles
- `application_db` - Loan applications
- `document_db` - Document metadata
- `admin_db` - Admin actions and reviews
- `notification_db` - User notifications

**Connection Details:**
- Host: `localhost:3307`
- Username: `root`
- Password: `root`

---

### 🔹 Environment Variables

Key environment variables (configured in docker-compose.yml):

```yaml
# JWT Configuration
JWT_SECRET: finflowsecretkeyforhs256algorithm
JWT_EXPIRATION: 3600000  # 1 hour in milliseconds

# Database
SPRING_DATASOURCE_URL: jdbc:mysql://mysql:3306/{db_name}
SPRING_DATASOURCE_USERNAME: root
SPRING_DATASOURCE_PASSWORD: root

# RabbitMQ
SPRING_RABBITMQ_HOST: rabbitmq
SPRING_RABBITMQ_USERNAME: guest
SPRING_RABBITMQ_PASSWORD: guest

# Service Discovery
EUREKA_CLIENT_SERVICEURL_DEFAULTZONE: http://eureka-server:8761/eureka
```

⚠️ **Production Note:** Change all default credentials before deploying to production!

---

### 🔹 Volume Management

Persistent data volumes:
- `mysql-data` - Database data
- `rabbitmq-data` - Message queue data
- `uploads-data` - Uploaded documents
- `grafana-data` - Grafana dashboards and settings

```bash
# List volumes
docker volume ls

# Remove all volumes (WARNING: deletes all data)
docker-compose down -v
```

---

## 🧪 API Testing

### Swagger UI (Interactive Documentation)

All services expose Swagger UI for interactive API testing:

```bash
# API Gateway Swagger (Aggregated)
http://localhost:8080/swagger-ui/index.html

# Individual Service Swagger
http://localhost:8081/swagger-ui/index.html  # Auth Service
http://localhost:8082/swagger-ui/index.html  # Application Service
http://localhost:8083/swagger-ui/index.html  # Document Service
http://localhost:8084/swagger-ui/index.html  # Admin Service
http://localhost:8085/swagger-ui/index.html  # Notification Service
```

---

### 🔹 API Endpoints Overview

#### **Auth Service** (`/auth`)

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| POST | `/auth/signup` | Create new user account | ❌ |
| POST | `/auth/login` | Login and get JWT token | ❌ |
| GET | `/auth/profile` | Get current user profile | ✅ |
| GET | `/auth/users` | Get all users (Admin only) | ✅ Admin |
| PUT | `/auth/users/{id}` | Update user profile | ✅ |

#### **Application Service** (`/applications`)

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| POST | `/applications` | Create loan application | ✅ |
| GET | `/applications` | Get all user applications | ✅ |
| GET | `/applications/{id}` | Get application by ID | ✅ |
| PUT | `/applications/{id}` | Update application | ✅ |
| DELETE | `/applications/{id}` | Delete application | ✅ |
| POST | `/applications/{id}/submit` | Submit application | ✅ |

#### **Document Service** (`/documents`)

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| POST | `/documents/upload` | Upload document | ✅ |
| GET | `/documents/application/{appId}` | Get all docs for application | ✅ |
| GET | `/documents/{id}` | Download document | ✅ |
| DELETE | `/documents/{id}` | Delete document | ✅ |

#### **Admin Service** (`/admin`)

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| GET | `/admin/applications` | Get all applications | ✅ Admin |
| GET | `/admin/applications/{id}` | Get application details | ✅ Admin |
| POST | `/admin/applications/{id}/decision` | Approve/Reject | ✅ Admin |
| PUT | `/admin/applications/{id}/status` | Update status | ✅ Admin |

#### **Notification Service** (`/notifications`)

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| GET | `/notifications` | Get user notifications | ✅ |
| GET | `/notifications/{id}` | Get notification by ID | ✅ |
| PUT | `/notifications/{id}/read` | Mark as read | ✅ |

---

### 🔹 Example API Calls

#### 1. User Signup
```bash
curl -X POST http://localhost:8080/auth/signup \
  -H "Content-Type: application/json" \
  -d '{
    "name": "John Doe",
    "email": "john@example.com",
    "password": "password123",
    "role": "APPLICANT"
  }'
```

#### 2. User Login
```bash
curl -X POST http://localhost:8080/auth/login \
  -H "Content-Type: application/json" \
  -d '{
    "email": "john@example.com",
    "password": "password123"
  }'

# Response:
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```

#### 3. Create Loan Application
```bash
curl -X POST http://localhost:8080/applications \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_JWT_TOKEN" \
  -d '{
    "amount": 50000,
    "purpose": "Home Renovation",
    "tenure": 36,
    "employmentType": "SALARIED",
    "monthlyIncome": 75000
  }'
```

#### 4. Upload Document
```bash
curl -X POST http://localhost:8080/documents/upload \
  -H "Authorization: Bearer YOUR_JWT_TOKEN" \
  -F "file=@/path/to/document.pdf" \
  -F "applicationId=1" \
  -F "documentType=ID_PROOF"
```

#### 5. Admin Approve Application
```bash
curl -X POST http://localhost:8080/admin/applications/1/decision \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer ADMIN_JWT_TOKEN" \
  -d '{
    "decision": "APPROVED",
    "comments": "All documents verified. Loan approved."
  }'
```

#### 6. Get Notifications
```bash
curl -X GET http://localhost:8080/notifications \
  -H "Authorization: Bearer YOUR_JWT_TOKEN"
```

---

### 🔹 Postman Collection

Import the API collection for easier testing:

1. Download [Postman](https://www.postman.com/downloads/)
2. Import the collection (if provided in `/postman` directory)
3. Set environment variables:
   - `BASE_URL`: `http://localhost:8080`
   - `JWT_TOKEN`: Your authentication token

---

## 📊 Key Features

### ✨ Microservices Architecture
- **Independent Services** - Each service is independently deployable and scalable
- **Service Discovery** - Automatic service registration with Eureka
- **Load Balancing** - Client-side load balancing with Spring Cloud LoadBalancer
- **API Gateway** - Single entry point with intelligent routing
- **Config Management** - Centralized configuration with Spring Cloud Config

### 🔐 Security & Authentication
- **JWT Authentication** - Stateless token-based authentication
- **Role-Based Access** - APPLICANT and ADMIN role segregation
- **Password Encryption** - BCrypt hashing algorithm
- **API Gateway Security** - Centralized authentication filter

### 📨 Event-Driven Architecture
- **Asynchronous Messaging** - RabbitMQ for event publishing and consumption
- **Loose Coupling** - Services communicate via events
- **Reliable Delivery** - Message persistence and acknowledgment
- **Scalable** - Event-driven design supports high throughput

### 📁 Document Management
- **File Upload** - Support for multiple document types
- **Document Verification** - Admin document review workflow
- **Secure Storage** - File system with metadata in database
- **Download Support** - Retrieve uploaded documents securely

### 🔔 Real-Time Notifications
- **Event-Based** - Automatic notifications on status changes
- **Persistent** - Stored in database for history
- **Read/Unread Status** - Track notification states
- **User-Specific** - Targeted notifications per user

### 📊 Monitoring & Observability
- **Health Checks** - Spring Boot Actuator endpoints
- **Metrics Collection** - Prometheus integration
- **Visualization** - Grafana dashboards
- **Distributed Tracing** - Zipkin for request flow analysis
- **Custom Metrics** - Business-specific metric tracking

### 🐳 DevOps Ready
- **Containerized** - Docker containers for all services
- **Orchestration** - Docker Compose for multi-container setup
- **Multi-Stage Builds** - Optimized Docker images
- **Health Checks** - Container-level health monitoring
- **Volume Management** - Persistent data storage

### 📝 API Documentation
- **OpenAPI 3.0** - Standard API specification
- **Swagger UI** - Interactive API testing interface
- **Auto-Generated** - Documentation from code annotations

### 🎯 Additional Features
- **Database per Service** - Each microservice has its own database
- **Graceful Degradation** - Services handle failures gracefully
- **CORS Support** - Cross-origin resource sharing enabled
- **Input Validation** - Request payload validation
- **Error Handling** - Consistent error response format
- **Logging** - Structured logging across services

---

## 🚀 Future Enhancements

### Planned Features
- [ ] **Loan Eligibility Engine** - Credit score calculation and eligibility checking
- [ ] **EMI Calculator** - Calculate monthly installments with interest
- [ ] **Repayment Module** - Track and manage loan repayments
- [ ] **Email/SMS Notifications** - Integration with SendGrid, Twilio
- [ ] **Redis Caching** - Improve performance with distributed caching
- [ ] **Advanced Search** - Elasticsearch integration for full-text search
- [ ] **File Storage** - AWS S3 or MinIO for document storage
- [ ] **CI/CD Pipeline** - GitHub Actions / Jenkins automation
- [ ] **Kubernetes Deployment** - Container orchestration at scale
- [ ] **API Rate Limiting** - Protect APIs from abuse

### Observability Improvements
- [ ] **Grafana Alerts** - Automated alerting for critical metrics
- [ ] **ELK Stack** - Centralized logging (Elasticsearch, Logstash, Kibana)
- [ ] **Distributed Tracing** - Enhanced Zipkin or Jaeger integration
- [ ] **Custom Dashboards** - Business-specific Grafana dashboards

### Security Enhancements
- [ ] **OAuth2 Integration** - Google, GitHub social login
- [ ] **2FA Authentication** - Two-factor authentication
- [ ] **API Key Management** - Service-to-service authentication
- [ ] **Secrets Management** - HashiCorp Vault integration
- [ ] **SSL/TLS** - HTTPS with certificate management

### Testing & Quality
- [ ] **Unit Tests** - JUnit 5 with Mockito
- [ ] **Integration Tests** - Testcontainers for database tests
- [ ] **Contract Testing** - Spring Cloud Contract
- [ ] **Load Testing** - JMeter or Gatling
- [ ] **SonarQube Analysis** - Automated code quality checks

---

## 🛠️ Troubleshooting

### Common Issues

#### 1. Port Already in Use
```bash
# Check what's using the port
netstat -ano | findstr :8080

# Kill the process (Windows)
taskkill /PID <process_id> /F

# Or change port in docker-compose.yml
ports:
  - "8090:8080"  # Use 8090 instead of 8080
```

#### 2. Services Not Starting
```bash
# Check logs
docker-compose logs -f <service-name>

# Restart specific service
docker-compose restart <service-name>

# Rebuild service
docker-compose up --build <service-name>
```

#### 3. Database Connection Issues
```bash
# Check MySQL health
docker-compose exec mysql mysqladmin ping -h localhost -proot

# Connect to MySQL
docker-compose exec mysql mysql -uroot -proot

# Verify databases exist
docker-compose exec mysql mysql -uroot -proot -e "SHOW DATABASES;"
```

#### 4. Services Not Registering with Eureka
- Wait 30-60 seconds for registration
- Check Eureka dashboard: `http://localhost:8761`
- Verify `EUREKA_CLIENT_SERVICEURL_DEFAULTZONE` in docker-compose.yml
- Check service logs for connection errors

#### 5. JWT Token Issues
- Token expired: Login again to get new token
- Invalid token: Check `JWT_SECRET` matches across services
- Missing token: Add `Authorization: Bearer <token>` header

#### 6. Out of Memory
```bash
# Increase Docker memory allocation
# Docker Desktop → Settings → Resources → Memory → 8GB+

# Or reduce services:
docker-compose up mysql rabbitmq eureka-server config-server auth-service api-gateway
```

---

## 📚 Documentation Links

- [Spring Boot Documentation](https://docs.spring.io/spring-boot/docs/current/reference/html/)
- [Spring Cloud Documentation](https://spring.io/projects/spring-cloud)
- [Docker Documentation](https://docs.docker.com/)
- [RabbitMQ Documentation](https://www.rabbitmq.com/documentation.html)
- [Prometheus Documentation](https://prometheus.io/docs/)
- [Grafana Documentation](https://grafana.com/docs/)

---

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

### Code Style
- Follow Java coding conventions
- Write meaningful commit messages
- Add comments for complex logic
- Update README if adding new features

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 👨‍💻 Author

**Mahesh Singh**

- GitHub: [@maheshsingh20](https://github.com/maheshsingh20)
- LinkedIn: [Connect with me](https://www.linkedin.com/in/mahesh-singh/)

---

## ⭐ Show Your Support

If you found this project helpful or learned something from it, please give it a ⭐ on GitHub!

---

## 📞 Contact

For questions, suggestions, or collaboration opportunities:
- Open an issue on GitHub
- Email: your.email@example.com

---

## 🙏 Acknowledgments

- Spring Boot Team for the amazing framework
- Spring Cloud for microservices tools
- Docker for containerization platform
- Open source community for inspiration and support

---

**Built with ❤️ using Spring Boot and Microservices Architecture**
