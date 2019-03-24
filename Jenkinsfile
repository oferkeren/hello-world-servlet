pipeline {
    agent any
    tools {
        maven "Maven"
    }
    stages {
        stage('checkout') {
            steps {
                deleteDir()
                checkout scm
            }
        } 
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
       stage('Move war to Tomcat') {
            steps {
                sh 'sudo rm -rf /opt/tomcat/webapps/helloworld'
                sh 'sudo rm /opt/tomcat/webapps/helloworld.war'
                sh 'sudo cp /var/lib/jenkins/workspace/igentifyTest/target/helloworld.war /opt/tomcat/webapps/'
                sh 'sudo systemctl restart tomcat'
            }
        } 
    }
  post {
     always {
         junit 'target/surefire-reports/*.xml'
         }
    }
}
