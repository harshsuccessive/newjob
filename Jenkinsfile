pipeline {
      agent any
	  tools {
	        maven 'maven-3'
			
	  }
      stages{
             stage('Build'){
                     steps{
                              sh script: 'mvn clean package'
                      }

                } 
             stage('Upload war to nexus'){
                     steps{
						 script{
                              def mavenPom = readMavenPom file: 'pom.xml'
                              nexusArtifactUploader artifacts: [
							         [
									      artifactId: 'samplesnap',
										  classifier: '',
										  file: "/var/lib/jenkins/workspace/Nexus-job/target/maven-snapshots-${mavenPom.version}.war",
										  type: 'war'
								    ]
							], 
				      			credentialsId: 'fc27c52e-aa44-4578-8490-c50aafc2b72e',
				      			groupId: 'com.jdevs',
				      			nexusUrl: '52.185.71.174:8081',
				      			nexusVersion: 'nexus3',
				      			protocol: 'http',
				      			repository: 'maven-snapshots',
				      			version: "${mavenPom.version}"
						 }
							}
                    }
         }
}		 
