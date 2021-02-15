pipeline {
  agent any
  stages{
       stage ('Build'){
        steps {
          sh 'mvn clean package'
        }
         post {
           success {
             echo 'Archiving...'
             archiveArtifacts artifacts:'**/target/*.war'
           }
         }
       }
       stage ('Deploy to Test'){
             steps {
               build job:'deploy_to_staging'
             }
           }
           stage ('Deploy to Prod') {
             steps {
               timeout(time:5, unit:'DAYS')
                 imput message: 'Approve Prod deployment?'
               }  
               build job:'deploy_to_prod'
             }     
           }
    }
} 
