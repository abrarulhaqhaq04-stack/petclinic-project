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
                echo "Building the project..."
            }
        }

        stage('Test') {
            steps {
                echo "Running tests..."
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying the application..."
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
