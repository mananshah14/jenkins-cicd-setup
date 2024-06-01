## jenkins-cicd-setup

To set up a Jenkins environment for Continuous Integration (CI) and Continuous Deployment (CD) with auto-scaling agents, Docker support, and basic CI checks, follow these steps with instructions to deploy thisin single step:-

### Prerequisites
- Docker installed on your local machine.
- Docker Compose installed on your local machine.

### Steps Overview:
  1. Set up Jenkins Master & auto-Scaling Agents to Handle Multiple CI/CD Pipelines
  2. Support docker based deployment & Basic CI Checks
  3. Demo Repository for Testing
    
    
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

1.5 Configure Jenkins Agent

1.5.1 Go to Manage Jenkins > Manage Nodes and Clouds.

1.5.2 Click on New Node.

1.5.3 Configure the agent with the following details:
   - Name: jenkins-agent
   - Remote root directory: /home/jenkins/agent
   - Launch method: Launch agent via Java Web Start.
   - Add the secret from the JENKINS_SECRET environment variable in the docker-compose.yml file.

1.5.3 Save and launch the agent.


2. Support docker based deployment & Basic CI Checks

2.1 Install Docker Pipeline Plugin

2.1.1 Go to Manage Jenkins > Manage Plugins.

2.1.2 Install the Docker Pipeline plugin.

2.2 Configure Jenkinsfile for Docker Deployment
In your Jenkinsfile, add steps to build, tag, and push Docker images, and deploy containers. Here's an example:
```
pipeline {
    agent {
        docker { image 'maven:3.8.1' }
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean compile'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Static Analysis') {
            steps {
                sh 'mvn checkstyle:check'
            }
        }
        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }
        stage('Docker Build') {
            steps {
                script {
                    dockerImage = docker.build("my-app:${env.BUILD_ID}")
                }
            }
        }
        stage('Docker Push') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub-credentials') {
                        dockerImage.push("${env.BUILD_ID}")
                        dockerImage.push("latest")
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker-compose up -d'
            }
        }
    }
    post {
        always {
            junit '**/target/surefire-reports/*.xml'
            archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
        }
    }
}
```


   






admin.
Configure Jenkins as needed and create your first pipeline using the demo repository.
Demo Repository:
A demo repository is provided at demo-repo/. You can set up your pipeline with the provided Jenkinsfile.

Usage
The Jenkins master is available at http://localhost:8080.
Jenkins agents will automatically scale to handle multiple jobs.
Stopping the Setup
To stop the Jenkins setup, run:

bash
Copy code
docker-compose down
shell
Copy code

### Final Folder Structure:
jenkins-cicd-setup/
├── docker-compose.yml
├── jenkins-master/
│ ├── Dockerfile
│ ├── plugins.txt
│ └── init.groovy.d/
│ └── basic-setup.groovy
├── jenkins-agent/
│ └── Dockerfile
├── demo-repo/
│ ├── Jenkinsfile
│ ├── README.md
│ ├── package.json
│ ├── src/
│ │ └── index.js
│ └── test/
└── README.md

arduino
Copy code

By following these instructions, you will have a fully functional Jenkins CI/CD environment 
