https://github.com/abrarulhaqhaq04-stack/petclinic-project.git

    pipeline {
    agent any

    environment {
        EC2_USER = 'ubuntu'
        EC2_HOST = '16.16.205.18'
        APP_NAME = 'petclinic.war'
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
                sh 'cp target/*.war target/$'petclinic.war''
            }
        }

        stage('Deploy') {
            steps {
                sshagent(credentials: ['ec2']) {

                    sh """
                    scp -o StrictHostKeyChecking=no \
                    target/$'petclinic.war' \
                    $'ubuntu@$'16.16.205.18':/tmp/

                    ssh -o StrictHostKeyChecking=no \
                    $ubuntu@$ \
                    'sudo cp /tmp/$'petclinic.war' /var/lib/tomcat10/webapps/
                     sudo systemctl restart tomcat10'
                    """
                }
            }
        }
    }
}
