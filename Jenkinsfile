pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/junhobangk/httpd.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t my-httpd .'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh 'docker run -d -p 80:80 --name my-httpd-container my-httpd'
            }
        }
    }
}
