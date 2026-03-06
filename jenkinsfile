pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                echo 'Building Website...'
            }
        }

        stage('Test') {
            steps {
                script {
                    if (fileExists('index.html')) {
                        echo 'Test Passed: index.html exists'
                    } else {
                        error 'Test Failed: index.html not found'
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying Website...'
                bat '''
                if not exist C:\\deploy-folder (
                    mkdir C:\\deploy-folder
                )
                xcopy /E /I /Y * C:\\deploy-folder
                '''
            }
        }

        stage('Start Server') {
            steps {
                echo 'Starting HTTP Server...'
                bat 'cd C:\\deploy-folder && python -m http.server 8000'
            }
        }

    }
}