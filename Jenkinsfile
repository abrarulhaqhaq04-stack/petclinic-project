pipeline {
    agent any

    stages {

        stage('Deploy to AWS') {
            steps {
                sshagent(credentials: ['ec2']) {
                    sh """
                    scp -o StrictHostKeyChecking=no target/app.war ubuntu@YOUR_EC2_PUBLIC_IP:/tmp/

                    ssh -o StrictHostKeyChecking=no ubuntu@YOUR_EC2_PUBLIC_IP '
                    sudo cp /tmp/app.war /var/lib/tomcat10/webapps/
                    sudo systemctl restart tomcat10
                    '
                    """
                }
            }
        }

    }
}
