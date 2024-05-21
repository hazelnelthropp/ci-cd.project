pipeline {
    agent any

    stages {
        stage('CheckOut') {
            steps {
                echo 'Checkout the source code from GitHub'
                git branch: 'main', url: 'https://github.com/hazelnelthropp/ci-cd.project.git'
            }
        }

        stage('Docker Image Creation') {
            steps {
                echo 'Building Docker images using Docker file'
                sh 'docker build -t hazelnelthropp/hazel-pro:v1 .'
            }
        }

        stage('Docker Login') {
            steps {
                echo 'Try to login to kranthi Docker hub'
                sh 'docker login -u hazelnelthropp -p Devops1624'
                sh 'docker push hazelnelthropp/hazel-pro:v1'
            }
        }

        stage('Push Image to DockerHub') {
            steps {
                echo 'Try to push new image to hazelnelthropp Docker Hub'
                sh 'docker push hazelnelthropp/hazel-pro:v1'
            }
        }

        stage('Deploy Application Ansible') {
            steps {
                echo 'Try to deploy Docker container in EC2 instance on port 5000'
                ansiblePlaybook credentialsId: 'ansible-ssh-key', disableHostKeyChecking: true, installation: 'ansible', inventory: '/etc/ansible/hosts', playbook: 'deploy.yaml'
            }
        }
    }
}
