pipeline {
    agent any

    tools {
        jdk 'JDK11'
        maven 'Maven3'
    }

    environment {
        TOMCAT_HOME = "/var/lib/tomcat10"
    }

    stages {

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                cp target/*.war $TOMCAT_HOME/webapps/HostelManagement.war
                '''
            }
        }
    }

    post {
        success {
            echo 'Application deployed successfully.'
        }

        failure {
            echo 'Build failed.'
        }
    }
}
