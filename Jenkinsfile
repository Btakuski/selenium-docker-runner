pipeline {
	agent any 
	stages {
		stage("Pull Latest Image") { 
			steps {
				    withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'pass', usernameVariable: 'user')]) {
                    sh "docker login --username=${user} --password=${pass}"
                    sh "docker pull btakuski/selenium-docker:latest"
                }
				
			}
		}
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
	}
	post { 
		always {
			archiveArtifacts artifacts: 'output/**'
			sh "docker-compose down"
		}
	}
}