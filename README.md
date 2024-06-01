## jenkins-cicd-setup

To set up a Jenkins environment for Continuous Integration (CI) and Continuous Deployment (CD) with auto-scaling agents, Docker support, and basic CI checks, follow these steps with instructions to deploy thisin single step:-

### Prerequisites
- Docker installed on your local machine.
- Docker Compose installed on your local machine.

### Steps Overview:
  1. Set up Jenkins Master & auto-Scaling Agents to Handle Multiple CI/CD Pipelines 
  2. Demo Repository for Testing which consists of docker based deployment & Basic CI Checks
    
    
### Detailed Steps:
1.  Set up Jenkins Master & auto-Scaling Agents to Handle Multiple CI/CD Pipelines
   
1.1 Create a Docker Network: This network will facilitate communication between your Jenkins master and agents.

```
docker network create jenkins
```
1.2 Create Docker Volume

```
docker volume create jenkins_data
```

1.3 Start Jenkins
Run the following command to start Jenkins:
```
git clone https://github.com/mananshah14/jenkins-cicd-setup.git
docker-compose up -d
```
1.4 Initial Jenkins Setup

1.4.1 Open your browser and navigate to http://localhost:8080.

1.4.2 Retrieve the initial admin password:
```
docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword
```
1.4.3 Complete the setup wizard and install suggested plugins.

1.4.4 Create an admin user when prompted.


2. Demo Repository for Testing which consists of docker based deployment & Basic CI Checks:

- Install Docker Pipeline Plugin
-  Go to Manage Jenkins > Manage Plugins.
- Install the Docker Pipeline plugin.

A demo repository is provided at demo-fe-be/. which consists of backend and frontend aplication of a 2 Tier application. You can build and test the microservices with the help of provided Jenkinsfile.

The Jenkins master is available at http://localhost:8080.Jenkins agents will automatically scale to handle multiple jobs.

#### Stopping the Setup

To stop the Jenkins setup, run:

```
docker-compose down
```
### Final Folder Structure:
```
jenkins-cicd-setup/
  ├── docker-compose.yml
  ├── demo-fe-be/
  │ ├── frontend
  │ │ ├──  docker-compose.yaml
  │ │ ├──  Dockerfile
  │ │ ├──  Jenkinsfile
  │ │ ├──  package.json
  │ │ ├── package-lock.json
  │ │ ├── public
  │ │ ├── README.md
  │ │ ├── src
  │ ├── backend
  │ │ ├── app.py
  │ │ ├── docker-compose.yaml
  │ │ ├──Dockerfile
  │ │ ├── Jenkinsfile
  │ │ ├── requirements.txt
  ├── README.md
```
