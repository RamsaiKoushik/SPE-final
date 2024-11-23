pipeline {
    agent any
    environment {
        DOCKER_CREDENTIALS_ID = 'docker-hub-credentials' // Jenkins credentials ID for Docker Hub
        DOCKER_HUB_REPO = 'ramsai987' // Docker Hub username or repo name
    }
    stages {
        stage('Clone Code') {
            steps {
                // Clone the repository
                git 'https://github.com/RamsaiKoushik/SPE-final' 
            }
        }
        stage('Build and Tag Images') {
            steps {
                script {
                    // Use Docker Compose to build images
                    sh """
                        sudo docker-compose -f docker-compose.yaml build \
                        --build-arg DOCKER_HUB_REPO=$DOCKER_HUB_REPO
                    """
                }
            }
        }
        stage('Push to Docker Hub') {
            steps {
                script {
                    // Login to Docker Hub and push images using docker-compose
                    docker.withRegistry('', DOCKER_CREDENTIALS_ID) {
                        sh """
                           sudo docker-compose -f docker-compose.yaml push
                        """
                    }
                }
            }
        }
        stage('Deploy with Docker Compose and Ansible') {
            steps {
                script {
                    // Optionally, use Ansible for deployment
                    ansiblePlaybook(
                        playbook: 'deploy.yml',
                        inventory: 'inventory',
                        credentialsId: 'ansible-ssh-credentials' // Jenkins SSH credentials ID
                    )
                }
            }
        }
        stage('Verify Workspace') {
            steps {
                sh 'ls -R'  // List all files in the workspace recursively
            }
        }
    }
}
