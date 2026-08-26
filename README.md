# Jenkins Docker Nginx Website

## Project Overview

This project demonstrates a simple CI/CD pipeline using Jenkins, Docker, GitHub, and Nginx.

A static HTML website is stored in a GitHub repository. Jenkins pulls the latest code, builds a Docker image, removes the old container, and deploys a new container with the updated website.

## Technologies Used

- Jenkins
- Docker
- GitHub
- Nginx
- HTML
- Ubuntu
- AWS EC2

## Project Workflow

GitHub → Jenkins → Docker Build → Remove Old Container → Run New Container → Deploy Website

## How It Works

1. The website source code is stored in GitHub.
2. Jenkins reads the `Jenkinsfile` from the repository.
3. Jenkins pulls the latest project files.
4. Docker builds a new image using the Dockerfile.
5. Jenkins removes the old Docker container.
6. Docker starts a new Nginx container.
7. The updated website is deployed and accessible through port 5000.

## Dockerfile

The Dockerfile uses the Nginx image and copies the HTML file into the Nginx web directory.

```dockerfile
FROM nginx:latest

COPY index.html /usr/share/nginx/html/index.html
