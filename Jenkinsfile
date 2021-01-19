pipeline {  
    agent any  
    stages {  
            stage ('Check-Git-Secrets') {  
                steps{
                    sh 'docker pull gesellix/trufflehog'
                    sh 'docker run -t gesellix/trufflehog --json https://github.com/devopssecure/webapp.git > trufflehog';
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

        stage ('Monitor') { 
           steps{ 
             echo "Now you can monitor!";
           }
        }
    }
}
