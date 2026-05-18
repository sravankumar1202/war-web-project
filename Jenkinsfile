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
			scannerHome = tool 'sonarqubescannerserver'
			}
		steps {
			withSonarQubeEnv('sonarqube server'){
			sh "${scannerHome}/bin/sonar-scanner"
	  			}
	 		}
		}
	}
}

