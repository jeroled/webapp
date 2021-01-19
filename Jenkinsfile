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

        stage ('Monitor') { 
           steps{ 
             echo "Now you can monitor!";
           }
        }
    }
}
