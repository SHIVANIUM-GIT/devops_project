pipeline {
    agent any
    stages {
        stage('SCM') {
            steps {
                git 'https://github.com/SHIVANIUM-GIT/devops_project.git'
            }
        }
        stage('Build dokcer OWN Image') {
            steps {
                sh "sudo docker build -t webpage:${BUILD_NUMBER} ."
            }
        }
    }
}
