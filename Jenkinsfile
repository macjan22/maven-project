pipeline {
  agent any
  triggers {
    pollSCM('*/5 * * * *')
  }
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
       stage ('Deployments') {
         parallel{
           stage ('Deploy to Test'){
             steps {
               sh "cp **/target/*.war /home/maks/dist/tomcat-test/webapps"
             }
           }
           stage ('Deploy to Prod') {
             steps {
               sh "cp **/target/*.war /home/maks/dist/tomcat-prod/webapps"
             }     
           }
         }
       }
    }
} 
  
