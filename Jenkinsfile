pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = 'sp-south-1'
        AWS_ACCESS_KEY_ID = ''
        AWS_SECRET_ACCESS_KEY = ''
        NGINX_DIR = '/usr/share/nginx/html/'
        EC2_PUBLIC_IP = '15.207.111.197'
        SSH_CREDENTIAL_ID = '786110' // Update with your credential ID
        GITHUB_REPO_URL = 'https://github.com/burhan121002/jn.git' // Update with your GitHub repository URL
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    // Check out the repository using the GitHub URL
                    git branch: 'main', url: GITHUB_REPO_URL
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    // Install Nginx (if not already installed)
                    sh 'sudo -S yum install nginx -y'  // Corrected usage of sudo -S
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Copy files to Nginx directory
                    sh "cp -r html/* $NGINX_DIR"

                    // Restart Nginx to apply changes
                    

                    // SSH into EC2 and run commands using the credential
                    withCredentials([file(credentialsId: SSH_CREDENTIAL_ID, variable: 'PRIVATE_KEY_FILE')]) {
                        sh "ssh -i $PRIVATE_KEY_FILE -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null ec2-user@$EC2_PUBLIC_IP 'sudo service nginx restart'"
                    }
                }
            }
        }
    }
}
