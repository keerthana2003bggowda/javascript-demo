### 3. Javascript

javascript-demo

A static HTML/JavaScript site, served by Nginx inside a Docker container, deployed via a Jenkins CI/CD pipeline to Docker Hub and an EC2 host.

What this application does

javascript-demo is a client-side-only web page (index.html + script.js) — no backend server, no build tooling, no framework. It's served as static content by Nginx.

Once deployed, the app is reachable at:

http://<host>:3000/

Tech stack
Frontend: Plain HTML +  JavaScript (no framework, no npm/build step)
Web server: Nginx (nginx:alpine)
Containerization: Docker (single-stage — just Nginx + static files)
CI/CD: Jenkins (declarative pipeline)
Registry: Docker Hub
Deployment target: AWS EC2 


Project structure
javascript-demo/
├── index.html                 # Main page
├── script.js                  # Client-side JavaScript
├── Dockerfile                 # Nginx-based static image build
├── Jenkinsfile                # without docker CI/CD pipeline (build → push → deploy)
├── JenkinsfileD                # Docker-based CI/CD pipeline (build → push → deploy)
├── .gitignore
└── README.md


