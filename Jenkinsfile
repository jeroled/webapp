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
                    sh 'mvn org.owasp:dependency-check-maven:check'
                    //sh 'rm owasp* || true'
                    //sh 'wget "https://raw.githubusercontent.com/jeroled/webapp/master/owasp-dependency-check.sh"'
                    //sh 'chmod +x owasp-dependency-check.sh'
                    //sh 'bash owasp-dependency-check.sh'
                    //sh 'cat /var/lib/jenkins/OWASP-Dependency-Check/odc-report/dependency-check-report.xml'
                    echo "Check complete";
                }
            }
        
            stage ('SonarQube Check'){
                steps {
                    withSonarQubeEnv('sonarqube'){
                        sh 'mvn sonar:sonar'
                        sh 'cat target/sonar/report-task.txt'
                    }
                }
            }
        
            stage('Build docker image') {
            //Build the docker image with a tag (qualys:sample in this case)
                steps {
                    dir("dockerbuild") {
                    sh "docker build -t qualys:sample . >
            docker_output"
                    }
                }
            }

            stage('Get Image id') {
 //Use the same repo:tag (qualys:sample in this case) combination with the grep command to get the same image id and save the image id in an environment variable
                steps {
                    script {
                        def IMAGE_ID = sh(script: "docker images | grep
                        -E '^qualys.*sample' | head -1 | awk '{print \$3}'", returnStdout:
                        true).trim()
                        env.IMAGE_ID = IMAGE_ID
                    }
                }
            }

            stage('Get Image Vulns - Qualys Plugin') {
            //Use the same environment variable(env.IMAGE_ID) as an input to Qualys Plugin's step
                steps {
                    getImageVulnsFromQualys useGlobalConfig:true,
                    imageIds: env.IMAGE_ID
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
