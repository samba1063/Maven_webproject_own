#!groovy

node('Own_Node'){
	   
	stage('Checkout'){

          checkout scm
       }

       stage('BuildArtifact'){
          // build step
          sh 'mvn clean package'
       }
	   
       
}
