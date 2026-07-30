pipeline {

    agent any

    tools {
        jdk 'JDK17'
        maven 'Maven3'
    }

    environment {
        TOMCAT_HOME="/opt/tomcat"
    }

    stages {

        stage('Git Checkout') {
            steps {
                git branch: 'main',
                url: 'https://github.com/cjayashri72-web/HostelManagment1.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Stop Tomcat') {
            steps {
                sh '''
                $TOMCAT_HOME/bin/shutdown.sh || true
                sleep 10
                '''
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                rm -f $TOMCAT_HOME/webapps/*.war
                cp target/*.war $TOMCAT_HOME/webapps/
                '''
            }
        }

        stage('Start Tomcat') {
            steps {
                sh '''
                $TOMCAT_HOME/bin/startup.sh
                sleep 15
                '''
            }
        }

    }

    post {

        success {
            echo "Deployment Successful"
        }

        failure {
            echo "Deployment Failed"
        }

    }

}
