pipeline {
     agent any
     stages {
         stage('Lint HTML')  { 
            steps  {
                 sh 'tidy -q -e *.html'
            }       
         } 
		stage('Security Scan') {
			steps { 
                 aquaMicroscanner imageName: 'alpine:latest', notCompliesCmd: 'exit 1', onDisallowed: 'fail', outputFormat: 'html'
              }
         }  
         stage('Upload to AWS')  {
            steps  {
                  withAWS(region:'eu-west-1',credentials:'UserC3') {
                  sh 'echo "Uploading content with AWS creds"'
                  s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, file:'index.html', bucket:'jenkinsabdullah')
                }
             }
         }
      }   
}      
