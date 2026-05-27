

# Docker & Docker Compose: End-to-End Containerization Assignment

This repository contains the source code and configuration files for a complete Docker containerization workflow. The project demonstrates the lifecycle of a web application from local development to containerization, multi-service orchestration, and publishing to a container registry.

## Project Objectives

* Install and verify Docker and Docker Compose.
* Containerize a simple web application (Python Flask) using a `Dockerfile`.
* Manage container lifecycles using the Docker CLI.
* Orchestrate a multi-container environment using `docker-compose.yml`.
* Manage images via Docker Hub (Push/Pull workflows).

---

## Step 1: Installation & Verification

Ensure you have Docker and Docker Compose installed on your system.

**1. Verify Installation**
Check the installed versions of Docker and the Compose plugin:

```bash
docker --version
docker compose version

```

**2. Test Docker Engine**
Run the official test container to confirm the Docker daemon is pulling and running images correctly:

```bash
docker run hello-world

```

---

## Step 2: Application Setup & Containerization

This project uses a lightweight Python Flask web application.

**1. Build the Docker Image**
Navigate to the directory containing the `Dockerfile` and application code, then build the image:

```bash
# Builds the image and tags it as 'flask-web-app'
docker build -t flask-web-app .

```

**2. Run the Container**
Start the container in detached mode and map port 5000 on your host to port 5000 in the container:

```bash
docker run -d -p 5000:5000 flask-web-app:latest

```

*The application will now be accessible at `http://localhost:5000`.*

---

## Step 3: Container Management (CLI Commands)

Use the following Docker CLI commands to interact with and manage the running application.

* **List running containers:** `docker ps`
* **List all containers (including stopped):** `docker ps -a`
* **Stop the container:** `docker stop my-running-app`
* **Start a stopped container:** `docker start my-running-app`
* **View container logs:** `docker logs my-running-app`
* **Inspect container details (networking, mounts, state):** `docker inspect my-running-app`
* **Remove the container:** `docker rm my-running-app` *(Note: The container must be stopped first, or use `-f` to force remove).*

---

## Step 4: Multi-Container Orchestration

To simulate a production environment, this project includes a `docker-compose.yml` file that defines multiple services (e.g., the web application and a backend database like Redis or MySQL).

**1. Bring up the services**
Start all services defined in the compose file in detached mode:

```bash
docker compose up -d

```

**2. Verify services are running**

```bash
docker compose ps

```

**3. Tear down the environment**
Stop and remove all containers, networks, and volumes created by Compose:

```bash
docker compose down

```

---

## Step 5: Docker Registry (Docker Hub)

This section demonstrates how to share the built image using a public Docker Hub registry.

**1. Authenticate with Docker Hub**

```bash
docker login

```

**2. Tag the Image**
Create a new tag pointing your local image to your Docker Hub repository:

```bash

docker tag flask-web-app:latest education1729/flask-web-app:latest

```

**3. Push the Image**
Upload the tagged image to Docker Hub:

```bash
docker push education1729/flask-web-app:v1.0

```

**4. Pull and Run Locally**
To verify the upload, remove the local copy of the image and pull it fresh from the registry:

```bash
# Remove local image
docker rmi <your-username>/flask-web-app:v1.0

# Pull from registry
docker pull <your-username>/flask-web-app:v1.0

# Run the pulled image
docker run -d -p 5000:5000 <your-username>/flask-web-app:v1.0

```
