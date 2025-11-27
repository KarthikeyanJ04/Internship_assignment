# MEAN Stack DevOps Task

This repository contains a full-stack MEAN application (MongoDB, Express, Angular, Node.js) deployed using Docker and GitHub Actions.

The application is containerized with Docker Compose and deployed to an AWS EC2 instance. It uses Nginx as a reverse proxy to route traffic on Port 80, eliminating CORS issues and serving as a single entry point.

## Project Structure
* **Frontend:** Angular 15 (Multi-stage Docker build served via Nginx Alpine)
* **Backend:** Node.js Express API
* **Database:** MongoDB 6.0
* **Proxy:** Nginx (Gateway)
* **CI/CD:** GitHub Actions (Build, Push, Deploy)

---

## Proof of Execution

### 1. CI/CD Configuration & Execution
**Description:** GitHub Actions workflow (`deploy.yml`) configuration and the successful execution logs showing all steps passing.

![CI/CD Config](https://github.com/KarthikeyanJ04/Internship_assignment/blob/master/screenshots/Screenshot%202025-11-28%20015806.png?raw=true)
<br>
![CI/CD Success](https://github.com/KarthikeyanJ04/Internship_assignment/blob/master/screenshots/Screenshot%202025-11-28%20023618.png?raw=true)

<br>
<br>

---

### 2. Docker Build & Push
**Description:** Build logs from the pipeline showing layer creation and verified images pushed to Docker Hub.

![Build Logs](https://github.com/KarthikeyanJ04/Internship_assignment/blob/master/screenshots/Screenshot%202025-11-28%20020211.png?raw=true)
<br>
![Docker Hub](https://github.com/KarthikeyanJ04/Internship_assignment/blob/master/screenshots/Screenshot%202025-11-28%20020245.png?raw=true)

<br>
<br>

---

### 3. Application Deployment
**Description:** Live application running on AWS EC2. The data shown proves the database connection is active (Picture taken on different browser cause Zen doesn't show url fully on screen at all times).

![Home Screen](https://github.com/KarthikeyanJ04/Internship_assignment/blob/master/screenshots/Screenshot%202025-11-28%20020340.png?raw=true)
<br>
![Working UI](https://github.com/KarthikeyanJ04/Internship_assignment/blob/master/screenshots/Screenshot%202025-11-28%20020452.png?raw=true)

<br>
<br>

---

### 4. Nginx Setup & Infrastructure
**Description:** The Nginx configuration (`nginx.conf`) showing the proxy logic, and `docker ps` output confirming the gateway is running on Port 80 and routing to internal services.

![Nginx Config](https://github.com/KarthikeyanJ04/Internship_assignment/blob/master/screenshots/Screenshot%202025-11-28%20021016.png?raw=true)
<br>
![Infrastructure](https://github.com/KarthikeyanJ04/Internship_assignment/blob/master/screenshots/Screenshot%202025-11-28%20021031.png?raw=true)

<br>
<br>

---

## Setup Instructions

### Prerequisites
* Docker & Docker Compose
* Node.js (for local dev)
* AWS EC2 (Ubuntu 22.04) for deployment

### Local Setup
1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/KarthikeyanJ04/Internship_assignment.git](https://github.com/KarthikeyanJ04/Internship_assignment.git)
    cd Internship_assignment
    ```

2.  **Start the services:**
    ```bash
    docker-compose up -d --build
    ```

3.  **Access the app:**
    * Frontend: `http://localhost`
    * API: `http://localhost/api`

### CI/CD Deployment
The project uses `.github/workflows/deploy.yml` for automated deployment.

1.  **Secrets Configuration:**
    Ensure the following secrets are set in the GitHub repository:
    * `DOCKER_USERNAME` / `DOCKER_PASSWORD`
    * `HOST_IP` (AWS Public IP)
    * `SSH_USER` (default: ubuntu)
    * `SSH_KEY` (PEM file content)

2.  **Trigger:**
    Pushing to the `master` branch triggers the pipeline. It builds the images, pushes to Docker Hub, copies the configuration files to the server via SCP, and restarts the containers.

### Manual Server Deployment (Optional)
If deploying manually without the pipeline:

1.  Install Docker on the VM:
    ```bash
    sudo apt update && sudo apt install docker.io docker-compose-v2 -y
    sudo usermod -aG docker $USER
    ```

2.  Copy `docker-compose.yml` and the `nginx/` folder to the server.

3.  Run the application:
    ```bash
    docker compose up -d
    ```