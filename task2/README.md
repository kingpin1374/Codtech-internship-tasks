## Project Flow
The pipeline follows a straightforward automated process:

Fetch Code: Pulls the latest source code from the repository.

Environment Setup: Prepares the Python environment and installs required libraries.

Deploy: Restarts the Flask application to apply the latest changes.

## System Requirements & Setup
### 1. Jenkins Installation (Ubuntu 24.04)
To avoid the GPG key errors common on the latest Ubuntu versions, Jenkins was installed using the new keyring method:

Bash
# Import the Jenkins GPG key correctly
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null

# Add the repository
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null

sudo apt update && sudo apt install jenkins -y
### 2. Python Environment
The EC2 instance requires Python 3 and pip to manage the application:

Bash
sudo apt install python3 python3-pip python3-venv -y
## Pipeline Configuration
The deployment is managed through a Shell Script or Jenkins Pipeline executing the following commands:

### Installation Stage
Bash
# Create and activate a virtual environment
python3 -m venv venv
source venv/bin/activate
# Install dependencies
pip install -r requirements.txt
### Deployment Stage
Bash
# Kill any existing process running on port 5000
fuser -k 5000/tcp || true
# Start the application in the background
nohup python3 app.py > app.log 2>&1 &
## Troubleshooting & Optimization
During the setup, we addressed several key issues to ensure the pipeline ran smoothly:

Sudo Permissions: We configured the /etc/sudoers file to allow the jenkins user to execute deployment commands without requiring a TTY (fixing the "sudo: a terminal is required" error).

Memory Management: To resolve the high memory usage (approx. 79%), we optimized the Jenkins process and ensured that old application processes were properly terminated before starting new ones.

GPG Key Errors: Fixed by manually importing the Jenkins signing key into the /usr/share/keyrings/ directory to comply with modern Ubuntu security standards.

## How to Run
Configure a "Freestyle Project" or "Pipeline" in Jenkins.

Link your Git repository.

Add the deployment shell commands to the Build Steps.

Run Build Now to deploy your Flask app to the EC2 instance.

Note: Screenshot of working webapp is also provided 
