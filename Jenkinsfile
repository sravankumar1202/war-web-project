pipeline {
	agent any
	environment {
	PATH = "/opt/maven/bin:$PATH"	
	}
	stages {
		stage ('buil') {
			steps {
			sh 'mvn clean install'
			}
		}
	}
}
