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
                    sh "sudo docker login -u shivanium -p ${docker_password}"
                    sh "sudo docker push docker.io/shivanium/webpage:${BUILD_NUMBER}"
                }             
            }
        }
        stage('Deploy Webapp in dev env') {
            steps {
                sh "sudo docker run -d -p 80:80 --name webpage docker.io/shivanium/webpage:${BUILD_NUMBER}"           
                sh 'sudo docker rm -f webpage'
            }
        }
    }
}
