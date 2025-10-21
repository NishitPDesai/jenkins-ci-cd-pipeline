Jenkins CI/CD Demo App

A simple Node.js app used to demonstrate a Jenkins pipeline with Docker.

Run Locally
```bash
docker build -t jenkins-simple-app .
docker run -d -p 3000:3000 jenkins-simple-app
