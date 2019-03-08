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
    }
    
}