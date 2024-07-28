pipeline {
    agent any
    stages {
        stage('SCM') {
            steps {
                git 'https://github.com/SHIVANIUM-GIT/devops_project.git'
            }
        }
        stage('Build Docker OWN Image') {
            steps {
                sh "sudo docker build -t docker.io/shivanium/webpage:${BUILD_NUMBER} ."
            }
        }
        stage('Push Image to Docker Hub') {
            steps {
                withCredentials([string(credentialsId: 'Dock_Pass', variable: 'docker_password')]) {
                    sh " docker login -u shivanium -p ${docker_password}"
                    sh " docker push shivanium/webpage:${BUILD_NUMBER}"
                }             
            }
        }
        stage('Deploy Webapp in dev env') {
            steps {
                sh "docker rm -f webpage"
                sh " docker run -d -p 8080:80 --name webpage shivanium/webpage:${BUILD_NUMBER}"           
            }
        }
        stage('Deploy on k8s') {
            steps {
                sh 'minikube start'
                sh "kubectl delete deployment mywebpage " 
                sh "kubectl create deployment mywebpage --image=shivanium/webpage:${BUILD_NUMBER}" 
                sh "kubectl scale deployment mywebpage --replicas=5" 
            }
        }
    }
}