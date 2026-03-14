================================================================================
PROJECT: UNIFORM WALA - CI/CD PIPELINE WITH JENKINS & KUBERNETES (KIND)
================================================================================
Author: Aman Sharma
Internship: DevOps Intern @ CODTECH IT SOLUTIONS
Date: March 2026

--------------------------------------------------------------------------------
1. PROJECT OVERVIEW
--------------------------------------------------------------------------------
This project demonstrates a complete DevOps Lifecycle for a Flask-based web 
application named "Uniform Wala." The project automates the entire process 
from code commit to production-ready deployment on a Kubernetes (Kind) 
cluster hosted on an AWS EC2 Ubuntu instance.

--------------------------------------------------------------------------------
2. TECHNOLOGIES USED
--------------------------------------------------------------------------------
- Version Control: Git & GitHub
- CI/CD Tool: Jenkins
- Containerization: Docker
- Orchestration: Kubernetes (Kind)
- Cloud Infrastructure: AWS (EC2)
- Framework: Python Flask

--------------------------------------------------------------------------------
3. PROJECT ARCHITECTURE & WORKFLOW
--------------------------------------------------------------------------------
1. CODE PUSH: Developer pushes code to the GitHub master branch.
2. AUTOMATION: Jenkins detects the change and triggers the Pipeline.
3. ENVIRONMENT SETUP: Jenkins ensures a Kind cluster is active on the server.
4. DOCKER BUILD: A Docker image (uniform-wala:local) is built from the source.
5. IMAGE LOADING: The image is side-loaded into the Kind cluster nodes.
6. K8S DEPLOYMENT: Deployment and Service manifests are applied via Kubectl.
7. HEALTH CHECK: Jenkins verifies the rollout status of the application pods.

--------------------------------------------------------------------------------
4. FILE STRUCTURE
--------------------------------------------------------------------------------
/task3
  |-- app.py               (Flask Application)
  |-- Dockerfile           (Multi-stage build instructions)
  |-- Jenkinsfile          (Groovy-based Pipeline script)
  |-- requirements.txt     (Python dependencies)
  |-- deployment.yaml      (K8s Deployment manifest with resource limits)
  |-- service.yaml         (K8s Service manifest)
README.txt                 (This documentation)

--------------------------------------------------------------------------------
5. PIPELINE STAGES SUMMARY
--------------------------------------------------------------------------------
- Cloning Repo: Pulls source code from GitHub using SSH/HTTPS credentials.
- Setup Environment: Validates the existence of the Kind cluster.
- Build Image: Compiles the Flask app into a Docker container.
- Load into Kind: Transfers the container image into the local K8s environment.
- Deploy: Applies Kubernetes manifests and monitors the rolling update.

--------------------------------------------------------------------------------
6. CHALLENGES & SOLUTIONS
--------------------------------------------------------------------------------
* ISSUE: "Permission Denied" for Docker API.
  SOLUTION: Added the 'jenkins' user to the 'docker' group and restarted Jenkins.

* ISSUE: "ImagePullBackOff" in Kubernetes.
  SOLUTION: Implemented 'imagePullPolicy: IfNotPresent' to force usage of the 
  locally loaded Kind image instead of searching Docker Hub.

* ISSUE: "Insufficient CPU" on EC2 t3.micro.
  SOLUTION: Optimized the deployment by lowering CPU requests to 100m and 
  reducing replicas to 1 to fit within instance resource constraints.

--------------------------------------------------------------------------------
7. HOW TO ACCESS THE WEB APP
--------------------------------------------------------------------------------
1. Run Port-Forwarding on EC2: 
   kubectl port-forward --address 0.0.0.0 service/uniform-wala-service 8081:80

2. Configure AWS Security Group:
   Open Port 8081 for Inbound Traffic (Source: 0.0.0.0/0).

3. Access via Browser:
   URL: http://<EC2-PUBLIC-IP>:8081

================================================================================
END OF DOCUMENT
================================================================================
