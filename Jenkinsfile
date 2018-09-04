#!groovy

node('New_Node'){
	stage('Checkout'){
        checkout scm
       }

       stage('BuildArtifact'){
          // build step
          sh 'mvn clean package'
	  emailext body: 'Stage has successfully build completed ', subject: 'jenkins Status', to: 'sambasiva1063@gmail.com'
       }
	stage('Deploy') {
	// Deploy the Artifacts into Tomcat Appserver
	sh 'mv /root/workspace/maven-mavenprojectstyle-owncode/target/*.war /opt/apache-tomcat-8.5.33/webapps/'
	sh 'rm -rf /opt/apache-tomcat-8.5.33/webapps/ROOT/*'	
	sh 'mv /opt/apache-tomcat-8.5.33/webapps/maven-mavenprojectstyle-owncode/* /opt/apache-tomcat-8.5.33/webapps/ROOT/'
	emailext body: 'Stage has successfully deploy completed ', subject: 'jenkins Status', to: 'sambasiva1063@gmail.com'
	}
	   
       
}
