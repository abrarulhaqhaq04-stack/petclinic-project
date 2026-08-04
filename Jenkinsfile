https://github.com/abrarulhaqhaq04-stack/petclinic-project.git

    pipeline {
    agent any

    environment {
        EC2_USER = "ubuntu"
        EC2_HOST = "YOUR_EC2_PUBLIC_IP"
        APP_NAME = "sample.war"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                url: 'https://github.com/abrarulhaqhaq04-stack/petclinic-project.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy') {
            steps {
                sshagent(credentials: ['aws-ssh-key']) {

                    sh """
                    scp -o StrictHostKeyChecking=no \
                    target/${APP_NAME} \
                    ${EC2_USER}@${EC2_HOST}:/tmp/

                    ssh -o StrictHostKeyChecking=no \
                    ${EC2_USER}@${EC2_HOST} \
                    'sudo cp /tmp/${APP_NAME} /var/lib/tomcat10/webapps/
                     sudo systemctl restart tomcat10'
                    """
                }
            }
        }
    }
}
