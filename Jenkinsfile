pipeline {
	agent {
		node {
			label "agent1"
		}
	}

	environment {
		AUTHOR = "Seno Wijayanto"
		EMAIL = "senowijayanto@gmail.com"
	}

  stages {
		stage("Prepare") {
			environment {
				APP = credentials("github-seno")
			}
			steps {
				echo("Author ${AUTHOR}")
				echo("Email ${EMAIL}")
				echo("Start Job: ${env.JOB_NAME}")
				echo("Start Build: ${env.BUILD_NUMBER}")
				echo("Branch Name: ${env.BRANCH_NAME}")
				echo("App User: ${APP_USR}")
				sh('echo "App Password: $APP_PSW" > "rahasia.txt"')
			}
		}

		stage("Build") {
			steps {
				echo("Start Build")
				sh("./mvnw clean compile test-compile")
				echo("Finish Build")
			}
		}

		stage("Test") {
			steps {
				script {
					def data = [
						"firstName": "Seno",
						"lastName": "Wijayanto"
					]
					writeJSON(file: "data.json", json: data)
				}

				echo("Start Test")
				sh("./mvnw test")
				echo("Finish Test")
			}
		}

		stage("Deploy") {
			steps {
				echo("Hello Deploy")
			}
		}
  }

  post {
    always {
      echo "I will always say Hello"
    }
    success {
      echo "Yay, success"
    }
    failure {
      echo "Oh no, failure"
    }
    cleanup {
      echo "Don't care success or error"
    }
  }
}