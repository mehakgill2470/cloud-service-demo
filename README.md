# Cloud Service Demo

## Purpose

Cloud Service Demo is a small sample website that represents an application that could later be hosted on a cloud platform.

## Files

- `index.html` - The sample web page for the cloud service.
- `README.md` - An overview of the project and its contents.
- `Dockerfile` - Instructions for packaging the webpage with Nginx.
- `kubernetes/deployment.yaml` - Creates and manages the application Pods.
- `kubernetes/service.yaml` - Provides access to the application Pods.

Version control helps a cloud project by tracking changes, preserving its history, and making team collaboration safer and easier.

## Docker and containerization

Docker packages an application and its runtime environment so it can run consistently on different computers. A Docker image is a lightweight, read only template that contains the application and its required environment. A Docker container is a lightweight, portable runtime instance created from that image.

## Build and run

Build the Docker image:

```bash
docker build -t cloud-service-demo:1.0 .
```

Run the container:

```bash
docker run -d --name cloud-demo-container -p 8080:80 cloud-service-demo:1.0
```

Open `http://localhost:8080` in a web browser to view the webpage.

## Kubernetes

Kubernetes is a platform used to deploy and manage containerized applications. A Pod runs the application container. A Deployment manages the Pods and keeps the requested number running. A Service provides a stable way to access the Pods.

Start Minikube and load the Docker image:

```bash
minikube start --driver=docker
minikube image load cloud-service-demo:1.0
```

Apply the Deployment and Service files:

```bash
kubectl apply -f kubernetes/deployment.yaml
kubectl apply -f kubernetes/service.yaml
```

Access the application locally:

```bash
kubectl port-forward service/cloud-service-demo 8080:80
```

While port forwarding is running, open `http://localhost:8080` in a web browser.
