# OpenUMS - Learning Management System

A comprehensive, microservices-based Learning Management System (LMS) built with modern technologies for educational institutions. OpenUMS provides a complete digital learning platform with features for course management, assessment, communication, material repository, and more.

## 🌟 Overview

OpenUMS is a modular, scalable LMS designed to handle the complex needs of educational institutions. The system is built using a microservices architecture, ensuring high availability, maintainability, and scalability. Each service is independently deployable and can scale based on demand.

## 🏗️ Architecture

The system follows a microservices architecture pattern with the following core components:

- **API Gateway** (KrakenD) - Centralized entry point for all client requests
- **Identity Service** - User authentication and authorization
- **Course Service** - Course and curriculum management
- **Assessment Service** - Assignments, quizzes, and grading
- **Material Repository** - File storage and content management
- **Notification Service** - Email and communication management
- **Chat Service** - Real-time messaging and communication
- **Class Scheduler** - Automated scheduling system
- **Frontend** - Vue.js-based user interface

## 🚀 Features

### Core Features

- **🔐 Authentication & Authorization**: Secure JWT-based authentication with role-based access control
- **📚 Course Management**: Complete course lifecycle management with departments, templates, and instances
- **📝 Assessment System**: Comprehensive assessment creation, submission, and grading
- **📁 Material Repository**: Secure file upload, storage, and sharing
- **💬 Real-time Chat**: Instant messaging for students and instructors
- **📧 Notifications**: Automated email notifications for important events
- **📅 Scheduling**: Intelligent class scheduling with conflict detection
- **👥 User Roles**: Support for Students, Instructors, Teaching Assistants, and Student Affairs

### Advanced Features

- **📊 Gradebook**: Comprehensive grade tracking and GPA calculation
- **🔄 Bulk Operations**: Efficient bulk user and course management
- **📱 Responsive Design**: Mobile-friendly interface
- **🌐 API Gateway**: Centralized API management with authentication
- **🐳 Containerized Deployment**: Docker-based deployment for easy scaling
- **📈 Performance Monitoring**: Built-in monitoring and logging

## 🛠️ Technology Stack

### Backend Services
- **Language**: Go (Golang)
- **Framework**: Gin, Echo
- **Database**: PostgreSQL, MongoDB, MySQL
- **Authentication**: JWT tokens
- **API Gateway**: KrakenD
- **Messaging**: Apache Pulsar, Redis
- **Containerization**: Docker & Docker Compose

### Frontend
- **Framework**: Vue.js 3
- **Build Tool**: Vite
- **Language**: TypeScript
- **State Management**: Pinia
- **Routing**: Vue Router
- **HTTP Client**: Axios
- **UI Components**: Custom components with modern design

### Infrastructure
- **Database Admin**: pgAdmin
- **File Storage**: Local filesystem with Docker volumes
- **Networking**: Docker networks for service communication
- **Development**: Hot reload and live development servers

## 📋 Prerequisites

Before running the project, ensure you have the following installed:

- [Docker](https://www.docker.com/get-started) and Docker Compose
- [Node.js](https://nodejs.org/) (version 16+)
- [Go](https://golang.org/dl/) (version 1.20+)
- [Git](https://git-scm.com/)

## 🚀 Quick Start

### Option 1: Automated Setup (Recommended)

Run the automated setup script that starts all services:

```bash
# Clone the repository
git clone <repository-url>
cd Gp

# Make the script executable (Linux/Mac)
chmod +x run_wholeProject.sh

# Run the complete system
./run_wholeProject.sh
```

**For Windows users**: Use Git Bash or WSL to run the bash script, or follow the manual setup below.

### Option 2: Manual Setup

1. **Create Docker Network**
   ```bash
   docker network create LMS
   ```

2. **Start Database Services**
   ```bash
   cd Identity
   docker compose up -d db pgadmin
   ```

3. **Start Identity Service**
   ```bash
   docker build -t identity .
   docker run --rm -p 8080:8080 --network LMS --name identity -d identity
   ```

4. **Start Assessment Service**
   ```bash
   cd ../Assesment
   docker compose up -d grade-service
   ```

5. **Start Other Services** (Follow similar pattern for each service)

6. **Start Frontend**
   ```bash
   cd ../frontend
   npm install
   npm run dev
   ```

## 🌐 Service URLs

Once all services are running, you can access them at:

| Service | URL | Description |
|---------|-----|-------------|
| **Frontend** | http://localhost:5173 | Main user interface |
| **API Gateway** | http://localhost:8000 | Centralized API endpoint |
| **Identity Service** | http://localhost:8080 | Authentication service |
| **Course Service** | http://localhost:8083 | Course management |
| **Assessment Service** | http://localhost:8085 | Assessment and grading |
| **Material Repository** | http://localhost:8089 | File management |
| **Notification Service** | http://localhost:8095 | Email notifications |
| **Chat Service** | http://localhost:8090 | Real-time messaging |
| **Database Admin** | http://localhost:8888 | pgAdmin interface |
| **Database** | localhost:5432 | PostgreSQL database |

## 📖 Service Documentation

Each service has its own detailed documentation:

- [Identity Service](./Identity/README.md) - User authentication and management
- [Assessment Service](./Assesment/README.md) - Assessment and grading system
- [Course Service](./Course/README.md) - Course and curriculum management
- [Material Repository](./Material-Repository/README.md) - File storage and management
- [Notification Service](./Notification/README.md) - Email notification system
- [Chat Service](./chat-service/) - Real-time messaging system
- [Class Scheduler](./Class-Scheduler/README.md) - Automated scheduling
- [API Gateway](./API-Gateway/) - Centralized API management

## 👥 User Roles

The system supports four main user roles:

1. **Student** - Can enroll in courses, submit assignments, view grades, access materials
2. **Instructor** - Can create courses, manage assessments, grade submissions, upload materials
3. **Teaching Assistant (TA)** - Can assist with grading and course management
4. **Student Affairs** - Can manage users, departments, and administrative functions

## 🔧 Development

### Running Individual Services

Each service can be run independently for development:

```bash
# Identity Service
cd Identity
go run main.go

# Assessment Service
cd Assesment
go run main.go

# Frontend
cd frontend
npm run dev
```

### Environment Configuration

Each service uses environment variables for configuration. Copy the `.env.example` files to `.env` and configure as needed:

```bash
# Example for Identity Service
cd Identity
cp .env.example .env
# Edit .env with your database credentials
```

### Database Setup

The system uses PostgreSQL as the primary database. The Identity service includes automatic migration:

```bash
# Database will be automatically migrated on first run
# Access pgAdmin at http://localhost:8888
# Default credentials: admin@admin.com / admin
```

## 🐳 Docker Configuration

The project includes Docker configurations for easy deployment:

- Each service has its own `Dockerfile`
- `docker-compose.yml` files for service orchestration
- Shared Docker network for inter-service communication
- Volume mounts for persistent data

## 🔒 Security

- JWT-based authentication with secure token handling
- Role-based access control (RBAC)
- API Gateway for centralized security
- bcrypt password hashing
- CORS configuration for secure frontend communication

## 📊 Monitoring & Logging

- Structured logging across all services
- Health check endpoints
- Performance monitoring capabilities
- Error tracking and reporting

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🆘 Support

If you encounter any issues or need help:

1. Check the individual service documentation
2. Review the logs using `docker logs <container-name>`
3. Ensure all services are running and healthy
4. Check network connectivity between services

## 🎯 Roadmap

- [ ] Mobile application development
- [ ] Advanced analytics and reporting
- [ ] Integration with external LMS systems
- [ ] Enhanced multimedia support
- [ ] AI-powered features
- [ ] Kubernetes deployment configurations

---

**Built with ❤️ for modern education**