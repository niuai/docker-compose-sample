
# Docker Compose Services Collection

A comprehensive collection of Docker Compose configurations for various infrastructure services, databases, monitoring tools, and development environments.

## 📋 Overview

This repository contains ready-to-use Docker Compose configurations for commonly used services. Each service is organized in its own directory with a self-contained `docker-compose` configuration file, making it easy to deploy individual services or combine them as needed.

## 🗂️ Available Services

### Databases

| Service | Directory | Port | Description |
|---------|-----------|------|-------------|
| **MySQL 5.6** | [`mysql/`](mysql/) | 3306 | MySQL database server (version 5.6) |
| **MySQL 8.0.23** | [`mysql-8.0.23/`](mysql-8.0.23/) | - | MySQL database server (version 8.0.23) |
| **PostgreSQL** | [`postgres/`](postgres/) | - | PostgreSQL database server |
| **Redis** | [`redis/`](redis/) | 6379 | Redis in-memory data structure store |

### Messaging & Streaming

| Service | Directory | Port | Description |
|---------|-----------|------|-------------|
| **Kafka** | [`kafka/`](kafka/) | 9092 | Apache Kafka with Zookeeper for distributed streaming |

### Monitoring & Logging

| Service | Directory | Ports | Description |
|---------|-----------|-------|-------------|
| **Prometheus** | [`prometheus/`](prometheus/) | 9090, 9100 | Prometheus monitoring system with Node Exporter |
| **ELK Stack** | [`elk/`](elk/) | 80, 443, 9200, 5044 | Elasticsearch, Logstash, Kibana with Nginx reverse proxy |
| **SkyWalking** | [`skywalking/`](skywalking/) | - | Application performance monitoring (APM) system |

### Development Tools

| Service | Directory | Port | Description |
|---------|-----------|------|-------------|
| **BaGet** | [`baget/`](baget/) | - | .NET NuGet server |
| **BitPlay** | [`bitplay/`](bitplay/) | - | Media streaming platform |
| **Grok** | [`grok/`](grok/) | - | Pattern matching and parsing tool |
| **Mind Map** | [`mind-map/`](mind-map/) | - | Mind mapping application |
| **Mattermost** | [`mattermost/`](mattermost/) | - | Open-source messaging platform |

### Big Data

| Service | Directory | Port | Description |
|---------|-----------|------|-------------|
| **HBase** | [`hbase/`](hbase/) | - | Apache HBase distributed database |
| **Spark** | [`spark/`](spark/) | - | Apache Spark unified analytics engine |

### Infrastructure

| Service | Directory | Port | Description |
|---------|-----------|------|-------------|
| **Registry** | [`registry/`](registry/) | - | Docker container registry |

## 🚀 Quick Start

### Prerequisites

- [Docker](https://docs.docker.com/get-docker/) installed
- [Docker Compose](https://docs.docker.com/compose/install/) installed

### Running a Service

Navigate to the desired service directory and start the containers:

```bash
# Example: Start MySQL
cd mysql
docker-compose up -d

# Example: Start Redis
cd redis
docker-compose up -d

# Example: Start Kafka
cd kafka
docker-compose up -d
```

### Stopping a Service

```bash
docker-compose down
```

### Viewing Logs

```bash
docker-compose logs -f
```

## 📝 Configuration Notes

### Common Patterns

- **Restart Policy**: Most services use `restart: unless-stopped` for automatic recovery
- **Volume Mounts**: Data directories are typically mounted to `./data` for persistence
- **Port Mapping**: Default ports are exposed for external access
- **Container Names**: Explicit container names are set for easier management

### Network Configuration

Some services (like `elk` and `prometheus`) use an external network named `internal-network`. Create it before starting these services:

```bash
docker network create internal-network
```

### Environment Variables

Default credentials and configurations are provided in each service's docker-compose file. **Important**: Change default passwords (e.g., MySQL root password `123456`) before using in production.

## 🔧 Usage Examples

### MySQL Database

```bash
cd mysql
docker-compose up -d

# Connect to MySQL
docker exec -it mysql mysql -u root -p123456
```

### Redis Cache

```bash
cd redis
docker-compose up -d

# Connect to Redis
docker exec -it redis redis-cli
```

### Kafka Messaging

```bash
cd kafka
docker-compose up -d

# Verify Kafka is running
docker-compose ps
```

### ELK Stack

```bash
# Create required network first
docker network create internal-network

cd elk
docker-compose up -d

# Access Kibana at http://localhost:5601
# Access Elasticsearch at http://localhost:9200
```

### Prometheus Monitoring

```bash
# Create required network first
docker network create internal-network

cd prometheus
docker-compose up -d

# Access Prometheus at http://localhost:9090
# Access Node Exporter metrics at http://localhost:9100
```

## 🛠️ Customization

Each service can be customized by modifying its `docker-compose.yaml` or `docker-compose.yml` file:

- **Change ports**: Modify the `ports` section
- **Update versions**: Change the `image` tag
- **Add volumes**: Mount additional directories
- **Set environment variables**: Add or modify the `environment` section
- **Configure networks**: Adjust network settings as needed

## 📊 Service Architecture

```
docker-compose/
├── baget/              # NuGet Server
├── bitplay/            # Media Platform
├── elk/                # ELK Stack + Nginx
├── grok/               # Pattern Matching
├── hbase/              # HBase Database
├── kafka/              # Kafka + Zookeeper
├── mattermost/         # Team Chat
├── mind-map/           # Mind Mapping Tool
├── mysql/              # MySQL 5.6
├── mysql-8.0.23/       # MySQL 8.0.23
├── postgres/           # PostgreSQL
├── prometheus/         # Prometheus + Node Exporter
├── redis/              # Redis
├── registry/           # Docker Registry
├── skywalking/         # APM System
└── spark/              # Apache Spark
```

## ⚠️ Important Notes

1. **Security**: Default configurations are for development purposes. Update passwords and security settings before production use.
2. **Data Persistence**: Most services mount local `./data` directories. Ensure these directories have appropriate permissions.
3. **Resource Limits**: Consider adding resource limits (`deploy.resources`) for production deployments.
4. **Backups**: Regularly backup persistent data stored in volume mounts.
5. **Updates**: Keep Docker images updated to latest stable versions for security patches.

## 🤝 Contributing

Feel free to:
- Add new service configurations
- Improve existing configurations
- Report issues or suggest enhancements
- Share best practices and usage tips

## 📄 License

This repository is provided as-is for educational and development purposes. Please review individual service licenses for production use.

## 🔗 Useful Links

- [Docker Documentation](https://docs.docker.com/)
- [Docker Compose Documentation](https://docs.docker.com/compose/)
- [Docker Hub](https://hub.docker.com/)

---

**Note**: This repository is continuously updated with new services and improvements. Check back regularly for updates!
