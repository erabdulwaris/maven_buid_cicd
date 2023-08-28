node(){

	//triggers { pollSCM 'H/5 * * * *' }
	
	//def sonarHome = tool name: 'SonarScanner', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
	
	stage('Code Checkout'){
		checkout changelog: false, poll: false, scm: scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'GitHubCred', url: 'https://github.com/erabdulwaris/Eshop.git']])
	}
	
	stage('Build Automation'){
		bat "mvn clean install -Dmaven.test.skip=true"
	}
	
	stage('Archive Artifacts'){
		archiveArtifacts artifacts: 'target/*.war'
	}
	
	stage('Code Deployment'){
		deploy adapters: [tomcat9(credentialsId: 'tomcatcrd', path: '', url: 'http://localhost:8080/')], contextPath: 'Eshop', onFailure: false, war: 'target/*.war'
	}
}
