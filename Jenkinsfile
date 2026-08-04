pipeline {
    agent any

    stages {

        stage('Deploy to AWS') {
            steps {
                sshagent(credentials: ['ec2']) {
                    sh """
                    scp -o StrictHostKeyChecking=no target/app.war ubuntu@16.16.205.18:/tmp/

                    ssh -o StrictHostKeyChecking=no ubuntu@16.16.205.18'
                    sudo cp /tmp/app.war /var/lib/tomcat10/webapps/
                    sudo systemctl restart tomcat10
                    '
                    """
                }
            }
        }

    }
}
