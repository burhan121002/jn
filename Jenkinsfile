pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout the source code from GitHub
                script {
                    git branch: 'main', url: 'https://github.com/burhan121002/jn.git'
                }
            }
        }

        stage('Build') {
            steps {
                // Install dependencies and run the Python application
                script {
                    
                    sh 'python app.py'
                }
            }
        }

        stage('Deploy') {
            steps {
                // Deploy stage (echo a message for demonstration)
                script {
                    echo 'Deployment successful! Your application is now deployed.'
                }
            }
        }
    }
}
