#!groovy

node('Slave12'){
	stage('Checkout'){
        checkout scm
       }

       stage('BuildArtifact'){
          // build step
          sh 'mvn clean package deploy'
	  slackSend 'Build Sucess '
       }
	stage('Deploy') {
	// Deploy the .war file into Tomcat Appserver
	sh 'mv /root/workspace/maven-mavenprojectstyle-owncode/target/*.war /opt/apache-tomcat-8.5.33/webapps/'
	sh 'rm -rf /opt/apache-tomcat-8.5.33/webapps/ROOT/*'	
	sh 'mv /opt/apache-tomcat-8.5.33/webapps/maven-web-project-1.0-SNAPSHOT/* /opt/apache-tomcat-8.5.33/webapps/ROOT/'
	slackSend 'Deployment Sucess '
	}
	   
       stage('S3bucket storage')
	{
		withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'sam_ec2', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) 
		s3Upload consoleLogLevel: 'INFO', dontWaitForConcurrentBuildCompletion: false, entries: [[bucket: 'samba-newstorage', excludedFile: '', flatten: false, gzipFiles: false, keepForever: false, managedArtifacts: false, noUploadOnFailure: false, selectedRegion: 'ap-south-1', showDirectlyInBrowser: false, sourceFile: '/opt/apache-tomcat-8.5.33/webapps/maven-web-project-1.0-SNAPSHOT.war', storageClass: 'STANDARD', uploadFromSlave: false, useServerSideEncryption: false]], pluginFailureResultConstraint: 'FAILURE', profileName: 'vicky_maggie', userMetadata: []
	}
}
