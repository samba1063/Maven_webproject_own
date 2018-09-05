#!groovy

node('New_Node'){
	stage('Checkout'){
        checkout scm
       }

       stage('BuildArtifact'){
          // build step
          sh 'mvn clean package'
	  slackSend 'Build Sucess '
       }
	stage('Deploy') {
	// Deploy the .war file into Tomcat Appserver
	sh 'mv /root/workspace/maven-mavenprojectstyle-owncode/target/*.war /opt/apache-tomcat-8.5.33/webapps/'
	sh 'rm -rf /opt/apache-tomcat-8.5.33/webapps/ROOT/*'	
	sh 'mv /opt/apache-tomcat-8.5.33/webapps/maven-web-project-1.0-SNAPSHOT/* /opt/apache-tomcat-8.5.33/webapps/ROOT/'
	slackSend 'Deployment Sucess '
	}
	   
       
}
