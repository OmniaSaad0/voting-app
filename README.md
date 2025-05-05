# 🗳️ Voting App

A cloud-native, containerized voting application deployed on Kubernetes.  
It allows users to cast votes between two options and view real-time results.  
This project demonstrates a microservices architecture, persistent state management, and inter-service communication using Redis and PostgreSQL.

---

## 📦 Project Structure

The application is composed of the following components:

- **Frontend (`vote`)**: A web UI where users can cast votes.
- **Worker (`worker`)**: A backend service that processes votes from Redis and stores them in PostgreSQL.
- **Result Display (`result`)**: A web UI that shows real-time vote counts.
- **Redis**: A message broker between the frontend and backend.
- **PostgreSQL (`db`)**: Stores vote counts persistently.

Each component is deployed using Kubernetes manifests.

---

## 📁 Repository Contents

| File | Description |
|------|-------------|
| `vote-namespace.yml` | Defines a custom namespace for the app |
| `vote-deployment.yml` / `vote-service.yml` | Frontend deployment and service |
| `worker-deployment.yml` | Backend vote processor |
| `result-deployment.yml` / `result-service.yml` | Real-time result display service |
| `redis-service.yml` / `redis-statefulset.yml` | Redis configuration |
| `db-secret.yml` / `db-service.yml` / `db-statefulset.yml` | PostgreSQL configuration and secrets |
| `variables.yml` | Contains common environment variables |

---

## 🚀 Deployment Instructions

> **Note:** Ensure you have a running Kubernetes cluster and `kubectl` installed and configured.

### 1. Create a Namespace
```bash
kubectl apply -f vote-namespace.yml
```

### 2. Deploy Redis
```bash
kubectl apply -f redis-service.yml
kubectl apply -f redis-statefulset.yml
```

### 3. Deploy PostgreSQL
```bash
kubectl apply -f db-secret.yml
kubectl apply -f db-service.yml
kubectl apply -f db-statefulset.yml
```

### 4. Deploy the Frontend (Vote App)
```bash
kubectl apply -f vote-deployment.yml
kubectl apply -f vote-service.yml
```

### 5. Deploy the Worker Service
```bash
kubectl apply -f worker-deployment.yml
```

### 6. Deploy the Result App
```bash
kubectl apply -f result-deployment.yml
kubectl apply -f result-service.yml
```

### 7. Verify the Deployments
```bash
kubectl get pods -n <your-namespace>
kubectl get services -n <your-namespace>
```

## 🧠 Key Concepts Demonstrated

- **Microservices Architecture**: Each app component runs independently as a microservice.
- **Stateful Services**: Redis and PostgreSQL are managed via StatefulSets.
- **Secrets Management**: Kubernetes Secrets are used to store sensitive data.
- **Service Communication**: Redis enables communication between the vote and worker services.
- **Environment Variables**: Externalized in `variables.yml` for flexibility and clarity.

---

## 📚 Related Resources

- [Example Voting App (Docker Samples)](https://github.com/dockersamples/example-voting-app)
- [Kubernetes Official Documentation](https://kubernetes.io/docs/)
