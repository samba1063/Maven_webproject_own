

node('Slave12'){
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
	sh 'mv  /root/workspace/maven-mavenprojectstyle-owncode/target/*.war /root/workspace/build/samba-${env.BUILD_NUMBER}.war'
	sh 'cp /root/workspace/build/samba-${env.BUILD_NUMBER}.war /opt/apache-tomcat-8.5.33/webapps/'
	sh 'rm -rf /opt/apache-tomcat-8.5.33/webapps/ROOT/*'	
	sh 'mv /opt/apache-tomcat-8.5.33/webapps/samba-${env.BUILD_NUMBER}/* /opt/apache-tomcat-8.5.33/webapps/ROOT/'
	slackSend 'Deployment Sucess '
	}
	   
       stage('S3bucket storage')
	{
	  s3Upload consoleLogLevel: 'INFO', dontWaitForConcurrentBuildCompletion: false, entries: [[bucket: 'samba-newstorage', excludedFile: '', flatten: false, gzipFiles: false, keepForever: false, managedArtifacts: false, noUploadOnFailure: false, selectedRegion: 'ap-south-1', showDirectlyInBrowser: false, sourceFile: '**/build/*.war', storageClass: 'STANDARD', uploadFromSlave: false, useServerSideEncryption: false]], pluginFailureResultConstraint: 'FAILURE', profileName: 'vicky_maggie', userMetadata: []
			

	}
}
