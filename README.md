# task-2-Jenkins-PP-CI-CD
# Jenkins CI/CD Pipeline for Node.js Dockerized Application

## Overview

This project contains a Jenkins pipeline configured to automate the CI/CD process for a Node.js application. The pipeline performs the following steps:

- **Build:** Installs Node.js dependencies using `npm install`.
- **Test:** Runs unit tests with `npm test`.
- **Docker Build:** Builds a Docker image for the application.
- **Docker Push:** Pushes the Docker image to Docker Hub.

---

## Prerequisites

- Jenkins server with pipeline plugin installed.
- Jenkins agent with Docker installed and configured.
- Jenkins user configured with NVM (Node Version Manager) and Node.js v16.20.2 installed.
- Docker Hub account with credentials stored in Jenkins credentials store (`dockerhub-password`).
- GitHub repository containing the application code and Jenkinsfile.

---

## Pipeline Details

- **Node.js version:** 16.20.2 managed via NVM.
- **Docker Image Name:** `jenkins-demo-app`
- **Docker Hub User:** `poojithareddy1620`

---

## How It Works

1. Jenkins clones the project from the GitHub repository.
2. The pipeline loads NVM and switches to Node.js version 16.
3. Runs `npm install` to install dependencies.
4. Executes tests via `npm test`.
5. Builds a Docker image with the tag `jenkins-demo-app`.
6. Logs into Docker Hub using stored Jenkins credentials.
7. Tags and pushes the Docker image to Docker Hub.
8. Logs out from Docker Hub.

---

## How to Use

1. Clone this repository in your Jenkins workspace.
2. Ensure Jenkins user has NVM and Node.js 16 installed at `/var/lib/jenkins/.nvm`.
3. Add Docker Hub credentials (`dockerhub-password`) in Jenkins Credentials.
4. Create a Jenkins pipeline job pointing to this repository.
5. Run the job to trigger the pipeline.

---

## Troubleshooting

- **NVM not found error:** Ensure NVM is installed for the Jenkins user at `$HOME/.nvm`.
- **Docker command errors:** Verify Jenkins agent can run Docker commands without sudo.
- **Login failures:** Check Docker Hub credentials in Jenkins.

---

## References

- [NVM Installation](https://github.com/nvm-sh/nvm)
- [Jenkins Pipeline Syntax](https://www.jenkins.io/doc/book/pipeline/syntax/)
- [Docker Hub](https://hub.docker.com/)
