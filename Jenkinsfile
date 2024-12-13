pipeline {
    
    environment {
        DOCKERHUB_CRED = credentials("Dockerhub-Credentials-ID") // Jenkins credentials ID for Docker Hub
        DOCKER_HUB_REPO = 'srinivasan2404' // Docker Hub username or repo name
        MINIKUBE_HOME = '/home/jenkins/.minikube'
        VAULT_PASS = credentials("ansible_vault_pass")
    }

    agent any
    stages {

        stage('Build and Tag Images') {
            steps {

                // dir('sql') {
                //     // sh "docker build -t ${DOCKER_HUB_REPO}/mysql:latest ."
                // }

                dir('spring-backend') {
                    sh "docker build -t ${DOCKER_HUB_REPO}/spring-backend:latest ."
                }

                dir('flutter-frontend/healthlink') {
                    // sh "cd flutter-front"
                    sh "docker build -t ${DOCKER_HUB_REPO}/flutter-web:latest ."
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                sh 'echo $DOCKERHUB_CRED_PSW | docker login -u $DOCKERHUB_CRED_USR --password-stdin'
                sh "docker push ${DOCKER_HUB_REPO}/spring-backend:latest"
                sh "docker push ${DOCKER_HUB_REPO}/flutter-web:latest"
                // sh "docker push ${DOCKER_HUB_REPO}/mysql:latest"
            }
        }

        stage('Clean Local Docker Images') {
            steps {
                sh "docker rmi ${DOCKER_HUB_REPO}/spring-backend || true"
                sh "docker rmi ${DOCKER_HUB_REPO}/flutter-web || true"
                // sh "docker rmi ${DOCKER_HUB_REPO}/mysql:latest || true"
            }
        }

        // stage('Deploy with Docker Compose and Ansible') {
        //     steps {
        //         script {
        //             // Optionally, use Ansible for deployment
        //             ansiblePlaybook(
        //                 playbook: 'deploy-app.yaml',
        //                 inventory: 'inventory',
        //                 // credentialsId: 'ansible-ssh-credentials' // Jenkins SSH credentials ID
        //             )
        //         }
        //     }
        // }

        stage("Deploy Ansible Vault with Kubernetes"){
            steps {
               sh '''
                echo "$VAULT_PASS" > /tmp/vault_pass.txt
                chmod 600 /tmp/vault_pass.txt
                ansible-playbook -i inventory.ini --vault-password-file /tmp/vault_pass.txt deploy_stack.yaml
                rm -f /tmp/vault_pass.txt
                '''
            }

        }
    }
}