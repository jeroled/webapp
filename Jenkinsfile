pipeline {  
    agent any  
    stages {  
            stage ('Git-Checkout') {  
                steps{
                    git url: 'https://github.com/jeroled/webapp.git'
                    echo "Checkout successful";
                } 
            }
            stage ('Compile') {  
                  steps{
                    sh 'mvn compile'
                    echo "test successful";
                    
                } 
            }
            stage ('Build') {  
                  steps{
                    sh 'mvn clean'
                    sh 'mvn package'
                    echo "build successful";
                    
                } 
            }
             stage ('Test') {  
                  steps{
                    sh 'mvn test'
                    echo "test successful";
                } 
            }
            
        stage ('Deploy') {
            steps{
            sshagent(['tomcat']) {
			sh 'scp -o StrictHostKeyChecking=target/*.war ubuntu@54.153.120.129:/home/ubuntu/prod/apache-tomcat-8.5.61/webapps/webapp.war'
            }
        }
        stage ('Monitor') { 
           steps{ 
             echo "Now you can monitor!";
           }
        }
    }
}
