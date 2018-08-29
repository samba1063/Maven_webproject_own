#!groovy

node {
	   
	stage('Checkout'){

          checkout scm
       }

       stage('BuildArtifact'){
          // build step
          sh 'mvn clean package'
       }
	   
       
}
