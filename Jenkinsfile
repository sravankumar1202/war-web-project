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
			sh "${scannerHome}/bin/qube-scanner"
	  			}
	 		}
		}
	}
}

