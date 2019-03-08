pipeline{
/* A Declarative pipeline */

agent any
    
    
    stages{
        stage('Build'){
            steps
            {
                bat 'mvn clean package'
            }
            post
            {
                success
                {
                    echo "Now Archiving.."
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
            }
        
        stage('Deploy To Staging'){
            steps
            {
                build job: 'Deploy_WebApp_Staging'
            }
        }
        
        stage('Deploy To Production'){
            steps
            {
                timeout(time:5,unit:'DAYS'){
                    input message:'Approve PRODUCTION deployment'
                }
                
                build job:'Deploy_WebApp_Prod'
            }
            
            post
            {
                success
                {
                    echo 'Code deployed to Production'
                }
                failure
                {
                    echo 'Deployment failed'
                }

            }
            }
        }
    }
    
