🧪 MLOPS - Dockerized Flask Application

This repository hosts a basic Flask web application packaged using Docker and deployed using a GitHub Actions CI/CD pipeline. This project serves as a foundational example for implementing modern Continuous Integration and Continuous Delivery practices.

🚀 Project Structure

The project directory is organized to separate the core application logic, testing, containerization instructions, and CI/CD workflow.
.
├── .github/
│   └── workflows/
│       └── cicd.yml           # GitHub Actions workflow for testing and publishing the Docker image.
├── mlops/                     # (Your virtual environment directory)
├── .gitignore                 # Files and directories to ignore in Git.
├── app.py                     # The main Flask application file.
├── DockerFile                 # Instructions for building the application's Docker image.
├── requirements.txt           # Python dependencies (Flask, pytest, etc.).
└── test_app.py                # Unit tests for the Flask application.


⚙️ Requirements & Local Setup
Prerequisites
-  Python 3.9+ (For running tests locally)
- Docker (For building and running the container)
- Git (For version control)


Running Locally (Non-Dockerized)
If you want to run the application directly on your host machine:
Activate Virtual Environment:
# Assuming you are using PowerShell on Windows
.\mlops\Scripts\Activate.ps1
# OR if using Bash/Linux/Git Bash
source mlops/bin/activate


Install Dependencies:
pip install -r requirements.txt


Run Tests:
pytest


Run Application:
python app.py


🐳 Dockerization
The application is containerized using the Dockerfile.
1. Build the Image
Use the Dockerfile to create a local image.
docker build -t flask-mlops-app:latest .


2. Run the Container
Run the image, mapping port 5000 inside the container to port 8080 on your host machine (or any port you prefer).
docker run -d -p 8080:5000 flask-mlops-app:latest


The application should now be accessible at http://localhost:8080.
☁️ CI/CD with GitHub Actions
This repository uses the workflow defined in .github/workflows/cicd.yml to automate testing and deployment.
Pipeline Stages
The CI/CD pipeline runs whenever code is pushed to the main branch or a pull request is opened against it. It consists of three dependent jobs:
build-and-test:
Checks out the code.
Sets up Python and installs dependencies (Flask, pytest).
Runs all unit tests (pytest). If tests fail, the pipeline stops.
build-and-publish:
Requires build-and-test to pass.
Logs into Docker Hub using GitHub Secrets (DOCKER_USERNAME, DOCKER_PASSWORD).
Builds the final Docker image.
Pushes the image to your Docker Hub repository: ${{ secrets.DOCKER_USERNAME }}/flasktest-app:latest.
Configuration (Secrets)
To enable the build-and-publish job, you must set the following secrets in your GitHub repository settings:
Secret Name
Purpose
DOCKER_USERNAME
Your Docker Hub username.
DOCKER_PASSWORD
Your Docker Hub Personal Access Token (PAT) for pushing images. (GitHub requires a PAT, not your actual password.)


