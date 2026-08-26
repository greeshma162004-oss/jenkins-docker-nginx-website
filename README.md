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

## How Docker Works in This Project

Docker packages the Nginx web server and the `index.html` website into a Docker image.

The Docker image is like a template containing everything needed to run the website.

Jenkins then creates a Docker container from this image. The container is the running instance where Nginx runs and serves the website.

Docker Image
    ↓
jenkins-nginx-website
    ↓
Docker Container
    ↓
jenkins-nginx-container
    ↓
Nginx runs inside the container
    ↓
Website is served

## Port Mapping

The Docker container is started using:

docker run -d --name jenkins-nginx-container -p 5000:80 jenkins-nginx-website

The `-p 5000:80` option maps two ports:

EC2 Server Port 5000 → Container Port 80

Port `80` is the default port where Nginx listens inside the Docker container.

Port `5000` is the port exposed on the EC2 server.

So when we open:

http://EC2-PUBLIC-IP:5000

The request follows this path:

Browser
   ↓
EC2 Public IP :5000
   ↓
EC2 Server Port 5000
   ↓
Docker Port Mapping
   ↓
Container Port 80
   ↓
Nginx
   ↓
index.html Website

This is why we use `5000:80`.

`5000` = Port on the EC2 server (host port)

`80` = Port inside the Docker container where Nginx is running (container port)
