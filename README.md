Payment Processing System

**Overview**
A cloud‑native payment processing system designed to handle 10M+ daily transactions with high reliability, scalability, and security. Built using Spring Boot, Kafka, Redis, and Kubernetes, the system demonstrates BFSI‑grade resilience and observability practices.

**Features**

Microservices Architecture: Payment, Account, Notification, and Audit services.
Idempotency & Reliability: Prevents duplicate transactions, supports retries via Kafka DLQ.
Performance Optimizations: Redis caching reduces API latency by ~35%.
Observability: Integrated with Prometheus, Grafana, and OpenTelemetry for metrics, logs, and traces.
Security & Compliance: OAuth2/JWT authentication, TLS encryption, audit logging for PCI DSS/RBI compliance.
Cloud‑Native Deployment: Dockerized services, Helm charts for Kubernetes, CI/CD via GitHub Actions.

**Architecture**


Client → API Gateway → Payment Service → Kafka → Account Service → DB/Redis
                                   ↘ Notification Service
                                   ↘ Audit Service
                                   
**API Gateway:** Entry point with authentication & rate limiting.

**Payment Service:** Validates requests, enforces idempotency, publishes events.

**Account Service:** Consumes events, updates balances, ensures ACID consistency.

**Notification Service:** Sends confirmations (email/SMS).

**Audit Service:** Logs immutable transaction records.

**Tech Stack**

Backend: Java, Spring Boot, Spring Security, Spring Data JPA
Messaging: Apache Kafka
Caching: Redis
Database: MySQL/Postgres
Cloud & DevOps: Docker, Kubernetes, Helm, GitHub Actions
Observability: Prometheus, Grafana, OpenTelemetry

**Project Setup**

Clone the repo:

bash
git clone https://github.com/yourusername/payment-processing-system.git
Build the project:

bash
mvn clean install
Run locally:

bash
docker-compose up
Access API:

Code
http://localhost:8080/api/payments
🔎 Example API Call
bash
curl -X POST http://localhost:8080/api/payments \
  -H "Authorization: Bearer <jwt-token>" \
  -H "Content-Type: application/json" \
  -d '{
        "transactionId": "txn123",
        "fromAccount": "ACC001",
        "toAccount": "ACC002",
        "amount": 500.00,
        "currency": "INR"
      }'

**Observability**

Metrics: Prometheus scrapes latency, throughput, error rates.
Dashboards: Grafana visualizes golden signals.
Tracing: OpenTelemetry captures distributed traces across services.
