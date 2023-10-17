pipeline{
    agent any
    stages{
        stage("getting code") {
            steps {
                git url: 'https://github.com/RouaMk/SpringBoot-App-SecondVersion.git', branch: 'main',
                credentialsId: 'github-credentials' //jenkins-github-creds
                sh "ls -ltr"
            }
        }

       //stage("Setting up infra") 
         stage("creation de image"){
            steps {                
                script {
                    echo "======== executing ========"
                        sh "mvn clean package"
            
                        sh "docker build -t devopstp ."
                       }            
                        }
                    } 
        stage("push to docker hub") {
            steps {                
                script {
                    echo "======== executing ========"
                        
                        sh "pwd"
                        sh "ls"
                        echo "push to hub"
                        sh "docker tag devopstp rouamk/devopstp:devopstp"
                        sh "docker push rouamk/devopstp:devopstp"
         
                           }        
                        }
                    }              
                }
            post{
                success{
                    echo "======== Setting up infra executed successfully ========"
                }
                failure{
                    echo "======== Setting up infra execution failed ========"
                }
            }
             
        }        
   /* 
    post{
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }*/
