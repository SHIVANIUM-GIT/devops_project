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
                sh "sudo docker build -t webpage:${BUILD_NUMBER} ."
            }
        }
        stage('Push Image to Docker Hub') {
            steps {
                withCredentials([string(credentialsId: 'Dock_Pass', variable: 'Dock_Pass')]) {
                    sh " sudo docker login -u shivanium --p ${Dock_Pass}"
                    sh "sudo docker push shivanium/webpage:${BUILD_NUMBER}"
                }
            }
        }
    }
}
