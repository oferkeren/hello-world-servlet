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
                sh 'rm -rf helloworld'
                sh 'rm helloworld.war'
                sh 'cp /var/lib/jenkins/workspace/helloWorld/target/helloworld.war /opt/tomcat/webapps/'
                sh 'systemctl restart tomcat'
            }
        } 
    }
  post {
     always {
         junit 'target/surefire-reports/*.xml'
         }
    }
}
