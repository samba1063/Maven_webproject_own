

node('node1'){
	stage('Checkout'){
        checkout scm
       }

       stage('BuildArtifact'){
          // build step
          sh 'mvn clean package'
	  slackSend 'build-${BUILD_NUMBER} Sucess '
       }
	stage('Deploy') {
	// Deploy the .war file into Tomcat Appserver
	sh "cd $WORKSPACE;/bin/mkdir build-${env.BUILD_NUMBER}/"
	sh "/bin/mv -f $WORKSPACE/target/*.war $WORKSPACE/build-${env.BUILD_NUMBER}/samba_${env.BUILD_NUMBER}.war"
	sh "/bin/cp $WORKSPACE/build-${env.BUILD_NUMBER}/samba_${env.BUILD_NUMBER}.war /opt/apache-tomcat-8.5.34/webapps/samba.war"
	sh "/bin/rm -rf /opt/apache-tomcat-8.5.34/webapps/ROOT/*"
	sh "/bin/mv /opt/apache-tomcat-8.5.34/webapps/samba/* /opt/apache-tomcat-8.5.34/webapps/ROOT/"
	slackSend 'Deployment-${env.BUILD_NUMBER} Sucess'
	}
	   
       stage('S3bucket storage')
	{
	  s3Upload consoleLogLevel: 'INFO', dontWaitForConcurrentBuildCompletion: false, entries: [[bucket: 'iphonestorage24', excludedFile: '', flatten: false, gzipFiles: false, keepForever: false, managedArtifacts: false, noUploadOnFailure: false, selectedRegion: 'us-east-1', showDirectlyInBrowser: false, sourceFile: '**build**/*.war', storageClass: 'STANDARD', uploadFromSlave: false, useServerSideEncryption: false]], pluginFailureResultConstraint: 'FAILURE', profileName: 'samba_iphone', userMetadata: []
		slackSend 'Uploaded ${env.BUILD_NUMBER} Sucess'	

	}
}
