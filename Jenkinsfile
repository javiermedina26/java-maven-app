pipeline{
	agent any
	tools {
		maven 'maven-3.9'
	}
	stages {
		stage("build jar") {
			steps {
				script {
					echo "building the application..."
					sh 'mvn package'
				}
			}
		}
		stage("build image") {
			steps {
				script {
					echo "building the docker image..."
					withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
						sh 'docker buildx -t javiermedina26/jmedina:jma-2.0 .'
						sh 'echo $PASS | docker login -u $USER --password-stdin'
						sh 'docker push javiermedina26/jmedina:jma-2.0'
					}
				}
			}
		}
		stage("deploy") {
			steps {
				script {
					echo "deploying the application..."
				}
			}
		}
	}
}
