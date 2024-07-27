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
               withCredentials([string(credentialsId: 'Dock_Pass', variable: 'dock_pass')]) {

                    sh "sudo docker login -u shivanium -p ${dock_pass}"
                    sh "sudo docker push docker.io/shivanium/webpage:${BUILD_NUMBER}"
                }             
                
            }
        }
    }
}
