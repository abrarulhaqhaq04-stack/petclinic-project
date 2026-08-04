pipeline {
    agent any

    environment {
        EC2_USER = "ubuntu"
        EC2_IP = "YOUR_EC2_PUBLIC_IP"
        APP_NAME = "sample.war"
    }

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/your-repository/sample-app.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy to AWS EC2') {
            steps {
                sshagent(['aws-ssh-key']) {
                    sh """
                    scp -o StrictHostKeyChecking=no target/${APP_NAME} ${EC2_USER}@${EC2_IP}:/tmp/

                    ssh -o StrictHostKeyChecking=no ${EC2_USER}@${EC2_IP} '
                    sudo cp /tmp/${APP_NAME} /opt/tomcat/webapps/
                    sudo systemctl restart tomcat
                    '
                    """
                }
            }
        }
    }

    post {
        success {
            echo "Application deployed successfully to AWS EC2."
        }

        failure {
            echo "Deployment failed."
        }
    }
}
