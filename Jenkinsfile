pipeline {
	agent any 
	stages {
		stage("Starting Grid") {
			steps {
				sh "docker-compose up -d hub chrome firefox"
			}
		}
		stage("Run Test") {
			steps {
				sh "docker-compose up --no-color home-page-module sign-in-module"
			}
		}

		stage("Stop Grid") {
			steps {
				sh "docker-compose down"
			}
		}
	}
}