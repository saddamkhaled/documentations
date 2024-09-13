
---

# Task Management App

This repository contains the **Task Management App**, developed using **Angular** for the frontend, along with several DevOps tools and monitoring solutions for continuous integration, containerization, and performance monitoring.

## 📋 Project Overview

The **Task Management App** is a web-based application built using **Angular** and **TypeScript**. It allows users to manage tasks efficiently by adding, updating, and deleting tasks. The application is designed to be responsive and user-friendly, with a focus on performance and scalability.

This project also integrates a full DevOps pipeline, including continuous integration, containerization, and system monitoring.

## 🛠️ Technical Stack

### **Frontend**
- **Angular**: Frontend framework for building the user interface.
- **TypeScript**: JavaScript superset used to build a more structured codebase.

### **DevOps & CI/CD Tools**
- **GitHub**: Code versioning and repository management.
- **GitHub Actions**: Automated CI/CD pipeline for testing, building, and deploying the application.
- **Docker**: Containerization of the application.
- **Docker Hub**: Storing and sharing Docker images.
- **Minikube**: Local Kubernetes environment for testing deployments.
- **Portainer**: Simplified management of Docker environments.
  
### **Monitoring Tools**
- **Node Exporter**: Collecting system metrics from containers.
- **Prometheus**: Collecting and storing metrics data for analysis.
- **Grafana**: Visualizing metrics and creating monitoring dashboards.

---

## 🚀 Getting Started

### Prerequisites
To run the project, ensure you have the following installed:
- **Node.js** and **npm**
- **Docker**
- **Minikube**
- **Kubectl**
- **Portainer** (optional)
- **Prometheus** and **Grafana** for monitoring

### Setup Instructions

#### 1. Clone the repository

```bash
git clone https://github.com/your-username/task-management-app.git
cd task-management-app
```

#### 2. Install Dependencies

```bash
npm install
```

#### 3. Running the Angular App Locally

```bash
ng serve
```

The app will be available at `http://localhost:4200`.

---

## 📦 Docker Containerization

#### 1. Build the Docker Image
To containerize the app, use Docker. First, create a Docker image by running the following command:

```bash
docker build -t your-dockerhub-username/taskmanagement:latest .
```

#### 2. Push the Image to Docker Hub

```bash
docker push your-dockerhub-username/taskmanagement:latest
```

#### 3. Running with Docker

```bash
docker run -d -p 80:80 your-dockerhub-username/taskmanagement:latest
```

This will run the app inside a Docker container and expose it on **port 80**.

---

## ⚙️ Kubernetes with Minikube

You can deploy the application on a local Kubernetes cluster using **Minikube**.

#### 1. Start Minikube

```bash
minikube start
```

#### 2. Deploy the App on Minikube

```bash
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```

You can access the app by getting the Minikube service URL:

```bash
minikube service taskmanagement --url
```

---

## 🔄 Continuous Integration / Continuous Deployment (CI/CD)

#### **GitHub Actions**

GitHub Actions is used for continuous integration. Each time a new commit is pushed to the repository, the following tasks are triggered:
- **Build**: The Angular app is built.
- **Dockerization**: The Docker image is built and pushed to Docker Hub.
- **Kubernetes Deployment**: The image is deployed to Minikube or any Kubernetes environment.

You can find the CI/CD pipeline configuration in the `.github/workflows` directory.

---

## 📊 Monitoring with Prometheus and Grafana

To monitor system performance and app usage, we use **Node Exporter**, **Prometheus**, and **Grafana**.

#### 1. Set Up Node Exporter
Node Exporter is deployed alongside the app to collect system metrics. It's configured in the Docker and Kubernetes environments.

#### 2. Deploy Prometheus

```bash
kubectl apply -f prometheus-deployment.yaml
```

#### 3. Deploy Grafana

```bash
kubectl apply -f grafana-deployment.yaml
```

Access **Grafana** and configure Prometheus as a data source, then create dashboards to visualize metrics.

---

## 📈 Performance Monitoring

- **Prometheus** collects the system and application-level metrics exposed by Node Exporter.
- **Grafana** visualizes these metrics for real-time monitoring, including CPU, memory usage, and request count.

---

## 👨‍💻 Contributing

Feel free to submit issues and pull requests for improvements. Follow the guidelines  for best practices.

---

## 📜 License

This project is licensed under the MIT License.

---

### Contact

For any questions or support, feel free to contact me at [saddambenkhaled@gmail.com].

---

This README provides a clear explanation of your project, including setup instructions, containerization, and monitoring tools used. It is ready to be published on GitHub!
