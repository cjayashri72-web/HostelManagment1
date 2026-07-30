pipeline { 
    agent any 
 
    tools { 
        jdk 'JDK11' 
        maven 'Maven3' 
    } 
 
    environment { 
        TOMCAT_HOME="/opt/tomcat" 
    } 
 
    stages { 
 
        stage('Checkout') { 
            steps { 
                git branch: 'master', 
                url: 'https://github.com/cjayashri72-web/HostelManagment1' 
            } 
        } 
 
        stage('Build') { 
            steps { 
                sh 'mvn clean' 
            } 
        } 
 
        stage('Test') { 
            steps { 
                sh 'mvn test' 
            } 
        } 
 
        stage('Package') { 
            steps { 
                sh 'mvn package' 
            } 
        } 
 
        stage('Deploy') { 
            steps { 
 
                sh ''' 
                cp target/*.war $TOMCAT_HOME/webapps/maven.war 
                ''' 
 
            } 
        } 
 
    } 
 
    post { 
 
        success { 
            echo "Application Deployed Successfully" 
        } 
 
        failure { 
            echo "Build Failed" 
        } 
 
    } 
 
}
