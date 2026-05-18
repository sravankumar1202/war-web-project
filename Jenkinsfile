
def registry = 'https://triallogs1l.jfrog.io'

pipeline {
    agent any
    environment {
        PATH="/opt/maven/bin:$PATH"
    }
    stages {
        stage('build') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('sonarqube analysis') {
	    environment {
		scannerHome = tool 'sonar-qube-scanner'
		}
	    steps {
		withSonarQubeEnv('sonar-qube-server') {
		sh 'mvn sonar:sonar -Dsonar.organization=sq01-key -Dsonar.host.url=https://sonarcloud.io'
		}
	    }
	}
	stage('War Publish') {
            steps {
                script {
                    echo "---------------- War Publish Started ----------------"
                    def version = sh(script: 'mvn help:evaluate -Dexpression=project.version -q -DforceStdout', returnStdout: true).trim()
                    def server = Artifactory.newServer url: registry + '/artifactory', credentialsId: 'artifact-credentials'
                    def properties = "buildid=${env.BUILD_ID}, commitid=${GIT_COMMIT}"
                    def uploadSpec = """{
                        "files": [
                            {
                                "pattern": "target/*.war",
                                "target": "sravan-libs-snapshot-local/in/irctc/www/irctc/${version}/",
                                "flat": "true",
                                "props": "${properties}",
				"exclusions": [ "*.sha1", "*.md5"]
			    }
			]
                    }"""
                    def buildInfo = server.upload(uploadSpec)
                    buildInfo.env.collect()
                    server.publishBuildInfo(buildInfo)
                    echo "---------------- War Publish Ended ----------------"
                }
            }
        }
    }
}













