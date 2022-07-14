pipeline{
    agent any
    environment {
        PATH = "$PATH:/opt/apache-maven-3.6.3/bin"
    }
    stages{
       stage('GetCode'){
            steps{
                git 'https://github.com/Araki678/mvn.git'
            }
         }        
       stage('Build'){
            steps{
                sh 'mvn clean package'
            }
         }

		stage('Code deploy') {
            steps{
				sshagent(['ec2-user-tomcat']) {
				  sh 'scp -o StrictHostKeyChecking=no target/01-maven-web-app.war ec2-user@65.1.130.145:/home/ec2-user/apache-tomcat-9.0.64/webapps'
				}
            }
        }
    }
}
