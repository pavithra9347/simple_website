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
                powershell 'New-Item -ItemType Directory -Force -Path C:\\deploy-folder'
                powershell 'Copy-Item -Recurse -Force * C:\\deploy-folder'
            }
        }

        stage('Start Server') {
            steps {
                echo 'Starting HTTP Server...'
                powershell 'Start-Process python -ArgumentList "-m http.server 8000" -WorkingDirectory "C:\\deploy-folder"'
            }
        }

    }
}