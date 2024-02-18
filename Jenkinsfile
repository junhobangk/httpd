pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git(branch: 'main', credentialsId: 'github_credential', url: 'https://github.com/junhobangk/httpd.git')
            }
        }

        stage('Check Docker Environment') {
            steps {
                script {
                    if (sh(script: 'docker info', returnStatus: true) != 0) {
                        error("Docker is not available. Please install and start Docker.")
                    }
                }
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

    post {
        success {
            echo 'Jenkins Pipeline finished successfully.'
        }
        
        failure {
            echo 'There was a problem with the Jenkins Pipeline.'
        }
        
        aborted {
            echo 'The Jenkins Pipeline was aborted.'
        }
    }
}
