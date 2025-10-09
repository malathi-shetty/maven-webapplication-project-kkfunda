node 
{
// /var/lib/jenkins/tools/hudson.tasks.Maven_MavenInstallation/maven-3.9.6/bin/
	def mavenHome=tool name: "maven-3.9.6"
	stage('git checkout')
	{
		git branch: 'development', url: 'https://github.com/malathi-shetty/maven-webapplication-project-kkfunda.git'
	}
	stage('Maven Build')
	{
		sh "${mavenHome}/bin/mvn clean package"
	}
	stage('SonarQube Report')
	{
		sh "${mavenHome}/bin/mvn sonar:sonar"
	}
	stage('Deploy into Nexus')
	{
		sh "${mavenHome}/bin/mvn deploy"
	}
	stage('Deploy to Tomcat') 
    {
     echo "Deploying WAR file using curl..." 

      sh """
      curl -u kk:password \
--upload-file /var/lib/jenkins/workspace/jio-dev-scriptedway-pipeline/target/maven-web-application.war \
"http://3.110.189.48:8080//manager/text/deploy?path=/maven-web-application&update=true"
          
        """
    }
}
