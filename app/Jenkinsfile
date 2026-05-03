pipeline {
    agent any

    environment {
        IMAGE_NAME = "shivushivu/devops-demo"
        TAG = "${BUILD_NUMBER}"
    }

    stages {

        stage('Clone Code') {
            steps {
                git 'https://github.com/shivanipunj/repo-testing.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat "docker build -t %IMAGE_NAME%:%TAG% ."
            }
        }

        stage('Login to DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'Docker-cred', 
                usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    bat "docker login -u %USER% -p %PASS%"
                }
            }
        }

        stage('Push Image') {
            steps {
                bat "docker push %IMAGE_NAME%:%TAG%"
            }
        }

        // stage('Run Container') {
        //     steps {
        //         bat "docker run -d -p 3000:3000 %IMAGE_NAME%:%TAG%"
        //     }
        // }
    }
}
