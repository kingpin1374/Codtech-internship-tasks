============================================================
CODTECH IT SOLUTIONS: DEVSECOPS INTERNSHIP REPORT
============================================================
Project: Task 4 - CI/CD Pipeline with Security Integration
Intern: Aman Sharma
Date: March 2026
------------------------------------------------------------

1. OBJECTIVE
The primary goal was to automate the build, deployment, and security 
testing of a web application using a modern DevSecOps pipeline. 
The focus was on ensuring 'Shift Left' security by integrating 
automated vulnerability scanning directly into the CI/CD flow.

2. TECHNICAL STACK
- CI/CD: Jenkins (Master Node)
- Containerization: Docker
- Orchestration: Kubernetes (KinD - Kubernetes in Docker)
- Security: OWASP ZAP (Dynamic Analysis)
- Cloud: AWS EC2 t3.small Instance
- SCM: GitHub

3. PIPELINE STAGES
- Cleanup: Automated 'docker system prune' to manage disk space.
- Cloning: Retrieval of source code and Kubernetes manifests from Git.
- Build & Load: Creation of application Docker image and injection 
  into the KinD cluster nodes.
- Deploy: Application of 'deployment.yaml' and 'service.yaml' to 
  expose the app on port 8081.
- DAST Scan: Automated security audit using OWASP ZAP to identify 
  runtime vulnerabilities.

4. TECHNICAL CHALLENGES & RESOLUTIONS
- DISK SPACE: The EC2 instance faced storage limits during the 
  heavy ZAP image pull. Resolved by implementing aggressive 
  pre-build cleanup stages and volume pruning.
- NETWORKING: Docker-to-Kubernetes communication was established 
  using '--network=host' and KinD port-mapping to ensure the scanner
  could reach the internal service.

5. HARDWARE LIMITATION NOTE (SONARQUBE)
Initially, the pipeline was designed to include Static Application 
Security Testing (SAST) via SonarQube. However, the current 
deployment environment is an AWS EC2 t3.small instance. Due to 
the intensive RAM and CPU requirements of the SonarQube engine 
(specifically the Elasticsearch and Compute Engine components), 
the instance was unable to maintain the service without crashing 
the Linux kernel. 

To ensure project delivery and pipeline stability, I pivoted the 
security strategy to focus on OWASP ZAP (DAST), which provides 
robust runtime security analysis within the existing hardware 
constraints.

6. RESULTS & CONCLUSION
The pipeline successfully deploys the 'Uniform-Wala' application 
to a production-like Kubernetes environment. The security scan 
was successfully integrated, and the 'zap_report.html' is archived 
for every build, meeting all internship requirements for Task 4.
============================================================
