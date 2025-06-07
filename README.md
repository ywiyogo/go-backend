# 🚀 Modern Go Backend

> **A production-ready REST API built with Go's standard library, designed for security, simplicity, and developer experience.**

## ✨ Core Values

🔒 **Security First** - CSRF protection, secure session management, and bcrypt password hashing  
⚡ **Performance** - Built on Go's efficient `net/http` with minimal external dependencies  
🔧 **Developer Experience** - Hot reloading, comprehensive testing, and Docker support  
🎯 **Flexibility** - Supports both password and OTP-based authentication flows  
📦 **Production Ready** - Rate limiting, proper error handling, and database migrations  

## 🎯 Key Features

- **Dual Authentication Modes**: Password-based or OTP-based authentication
- **Session Management**: Secure cookie-based sessions with CSRF protection
- **Hot Reloading**: Instant feedback during development with Air
- **Comprehensive Testing**: Unit and integration tests with Docker test environment
- **Database Integration**: PostgreSQL with migrations and type-safe queries (sqlc)
- **Rate Limiting**: Built-in protection against abuse
- **RESTful API**: Clean endpoints for notes management and authentication

## 🛠 Tech Stack

- **Runtime**: Go (standard library focused)
- **Database**: PostgreSQL
- **DevOps**: Docker Compose, Air (hot reload)
- **Database Tools**: golang-migrate, sqlc
- **Build Tool**: Make

## 🚀 Quick Start

### 1. Start the Application
```bash
# Start database and backend with hot reloading
docker compose --env-file .env up -d

# Run database migrations
migrate -path internal/db/migrations -database "postgres://${DB_USER}:${DB_PASSWORD}@localhost:5432/${DB_NAME}?sslmode=disable" up
```

### 2. Test the API
```bash
# Register a new user
curl -X POST http://localhost:8080/register -d "email=user@example.com" -d "password=mypassword123"

# Login and get session
curl -X POST http://localhost:8080/login -d "email=user@example.com" -d "password=mypassword123" -c cookies.txt

# Access protected dashboard
curl -X POST http://localhost:8080/dashboard -H "X-CSRF-Token: YOUR_TOKEN" -b cookies.txt
```

## 🧪 Testing

```bash
# Run all tests
make test

# Unit tests only
make test-unit

# Integration tests with Docker
make test-integration

# Integration tests with coverage
make test-integration-coverage
```

## 🔧 Development Commands

```bash
# Build the application
make build

# Run without Docker
make run

# View application logs
docker compose logs

# Clean up Docker resources
docker compose down --rmi local -v
```

## 📁 Project Structure

```
├── internal/
│   ├── api/          # HTTP handlers and routing
│   ├── auth/         # Authentication service and repository
│   ├── db/           # Database migrations and queries
│   └── notes/        # Notes management features
├── test/             # Integration tests and Docker setup
├── docs/             # Documentation (auth workflow, etc.)
└── docker-compose.yml
```

## 🔐 Authentication Modes

### Password Mode (`OTP_ENABLED=false`)
Traditional email/password authentication with secure session management.

### OTP Mode (`OTP_ENABLED=true`)
Email-based one-time password authentication for enhanced security.

> **Detailed authentication workflow**: See [docs/auth_workflow.md](./docs/auth_workflow.md)

---

**Ready to build something amazing?** This backend provides a solid foundation for any application requiring secure authentication and data management. 🎉