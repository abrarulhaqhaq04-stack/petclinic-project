pipeline {
    agent any

    tools {
        maven 'maven'
        jdk 'JAVA_HOME'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/devopsplan2026/petclinic-project.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Deploy') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'tomcat',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS'
                )]) {

                    sh '''
                    curl -u $USER:$PASS \
                    --upload-file target/petclinic.war \
                    "http://localhost:8089/manager/text/deploy?path=/petclinic&update=true"
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

