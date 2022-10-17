pipeline {
	agent {
		node {
			label "agent1"
		}
	}
  stages {
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