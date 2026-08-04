pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo "Source code is checked out from SCM automatically."
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                echo "Running tests..."
            }
        }

        stage('Deploy') {
            steps {
                sh 'cp target/*.war/opt/tomcat/webapps/'
            }
        }
    
    }

    post {
        always {
            echo "Pipeline execution completed."
        }

        success {
            echo "Build was successful."
        }

        failure {
            echo "Build failed."
        }
    }
}
