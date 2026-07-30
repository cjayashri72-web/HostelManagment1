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
                git branch: 'master',
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
        rm -rf $TOMCAT_HOME/webapps/HostelManagementSystem*
        cp target/*.war $TOMCAT_HOME/webapps/
        '''
    }
}

stage('Start Tomcat') {
    steps {
        sh '''
        chmod +x $TOMCAT_HOME/bin/*.sh
        $TOMCAT_HOME/bin/startup.sh
        sleep 15
        '''
    }
}
