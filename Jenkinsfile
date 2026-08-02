pipeline {
    agent any

    tools {
        maven 'maven'
        jdk 'java'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/devopsplan2026/petclinic-project.git'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean package -DskipTests'
            }
        }

        stage('Deploy') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'eed2b10a-9343-4bbf-97da-d03e1542b9b8',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS'
                )]) {

                    bat'''
                    curl -u $USER:$PASS \
                    --upload-file target/petclinic.war \
                    "http://localhost:8081/manager/text/deploy?path=/petclinic&update=true"
                    '''
                }
            }
        }
    }

    post {

        success {
            echo 'Deployment Successful!'

            
        }

        failure {
            echo 'Deployment Failed!'

        }
    }
}

