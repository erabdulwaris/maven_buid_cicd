node(){

	//def sonarHome = tool name: 'SonarScanner', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
	
	stage('Code Checkout'){
		checkout changelog: false, poll: false, scm: scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'GitHubCred', url: 'https://github.com/erabdulwaris/Hello.git']])
	}
	
	stage('Build Automation'){
		bat "mvn clean install -Dmaven.test.skip=true"
	}
	
	stage('Archive Artifacts'){
		archiveArtifacts artifacts: 'target/*.war'
	}
	
	stage('Code Deployment'){
		deploy adapters: [tomcat9(credentialsId: 'tomcatcrd', path: '', url: 'http://192.168.100.62:8080/')], contextPath: 'hello', onFailure: false, war: 'target/*.war'
	}
}
