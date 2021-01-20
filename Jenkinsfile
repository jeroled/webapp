pipeline {  
    agent any  
    stages {  
            stage ('Check-Git-Secrets') {  
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
        
            stage ('OWASP Dependency Check'){
                steps {
                    sh 'wget "https://raw.githubusercontent.com/jeroled/webapp/master/owasp-dependency-check.sh"'
                    sh 'chmod +x owasp-dependency-check.sh'
                    sh 'bash owasp-dependency-check.sh'
                    sh 'cat /var/lib/jenkins/OWASP-Dependency-Check/reports/dependency-check-report.xml'
                    echo "Check complete";
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
