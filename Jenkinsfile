pipeline {
	agent any
	environment {
	PATH = "/opt/maven/bin:$PATH"	
	}
	stages {
		stage ('build') {
			steps {
			sh 'mvn clean install'
			}

		}

		stage('sonarqube analysis') {
		environment {
			scannerHome = tool 'sonar-qube-scanner'
			}
		steps {
			withSonarQubeEnv('sonar-qube-server'){
			sh 'mvn sonar:sonar -Dsonar.organization=sq01-key -Dsonar.host.url=https://sonarcloud.io'
	  			}
	 		}
		}
	}
}

