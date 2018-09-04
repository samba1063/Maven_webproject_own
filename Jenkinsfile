#!groovy

node('New_Node'){
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
	sh 'rm -rf /opt/apache-tomcat-9.0.10/webapps/ROOT/*'	
	sh 'mv /opt/apache-tomcat-9.0.10/webapps/maven-web-project-1.0-SNAPSHOT/* /opt/apache-tomcat-9.0.10/webapps/ROOT/'
	}
	   
       
}
