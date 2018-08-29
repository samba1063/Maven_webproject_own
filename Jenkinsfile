#!groovy

node('Own_Node'){
	   
	stage('Checkout'){

          checkout scm
       }

       stage('BuildArtifact'){
          // build step
          sh 'mvn clean package'
       }
	stage('Deploy') {
	// Deploy the Artifacts into Tomcat Appserver
	sh 'mv /root/workspace/Maven_PipeLine_Own_Webproject/target/*.war /opt/apache-tomcat-9.0.10/webapps/'
	}
	   
       
}
