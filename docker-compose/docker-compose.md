# docs
Alexandria project architecture and documentation

## docker compose setup
This guide will help you set up and run a variety of services using Docker Compose.

### Prerequisites
Before you begin ensure you have the following requirements:

- [docker, docker compose](https://docs.docker.com/get-docker) installed.

- **ports available**: Each service is mapped to specific ports as defined in the Docker Compose file. Ensure these ports are available on your host machine.

### Services Overview
This Docker Compose setup includes the following services:

- Redis (v6.2, Alpine): A key-value store used for caching and as a message broker.
- MongoDB (v4.4): A NoSQL database for storing JSON-like documents.
- RabbitMQ (v3.7.28, Management): A messaging broker that facilitates the efficient communication between different parts of the application.
- NATS (v2.9.22, Alpine): A lightweight, high-performance messaging system for microservices.
- Milvus (v2.3.3): A powerful open-source vector database for AI applications.
    - Includes etcd for distributed configuration and service discovery.
    - MinIO for object storage.
- HttpBin (kennethreitz/httpbin): A simple HTTP request & response service.

### Configuration

#### Environment Variables
You can modify environment variables for the Docker Compose configuration. These can be defined in a .env file located at the root of your project directory.

Example .env File
```bash
# General settings
DOCKER_VOLUME_DIRECTORY=./data

# Redis configuration
REDIS_PASSWORD=your_redis_password

# MongoDB configuration
MONGO_INITDB_ROOT_USERNAME=admin
MONGO_INITDB_ROOT_PASSWORD=admin

# RabbitMQ configuration
RABBITMQ_ERLANG_COOKIE=secret_cookie
RABBITMQ_DEFAULT_USER=admin
RABBITMQ_DEFAULT_PASS=admin

# MinIO configuration
MINIO_ACCESS_KEY=minioadmin
MINIO_SECRET_KEY=minioadmin
```

#### Volumes
Persistent data for services like MongoDB, Redis, and RabbitMQ is stored in Docker volumes. The default path is set to ./volumes/[service_name] but can be customized via the DOCKER_VOLUME_DIRECTORY environment variable.

### Running the Services
To start all services, use the following command:
```bash
docker-compose up -d
```
If you make changes to the configuration and want to force a recreation of the services, use:
```bash
docker-compose up -d --force-recreate
```

### Troubleshooting
If you encounter any issues, refer to the service logs using:
```bash
docker-compose logs [service_name]
```
