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
                withCredentials([string(credentialsId: 'Dock_Pass', variable: 'Dock_Pass')]) {
                    sh "echo ${Dock_Pass} | sudo docker login -u shivanium --password-stdin"
                    sh "sudo docker push docker.io/shivanium/webpage:${BUILD_NUMBER}"
                }
            }
        }
    }
}
