//DECLARATIVE

pipeline {
	agent any
	// agent { docker { image 'maven:3.6.3'}}
	environment {
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages {
		stage('Checkout') {
			steps {
				echo "Build"
				sh 'docker version'
				sh 'mvn --version'
				echo "Path - $PATH"
				echo "Build number- $BUILD_NUMBER"
				echo "Build TAG- $BUILD_TAG"
				echo "Build_url - $BUILD_URL"
			}
		}
		stage('Compile') {
			steps {
				sh 'mvn clean compile'
			}
		}
		stage('Test') {
			steps {
				sh 'mvn test'
			}
		}
		stage('Integration Test') {
			steps {
				sh 'mvn failsafe:integration-test failsafe:verify'
			}
		}
		stage('Package') {
			steps {
				sh 'mvn package -DskipTests'
			}
		}
		stage('Build Docker Image') {
			steps {
				//"docker build -t yashkasat32/currency-exchange-devops:$env.BUILD_TAG"
				script {
					dockerImage = docker.build("yashkasat32/currency-exchange-devops:${env.BUILD_TAG}")
				}
			}
		}
		stage('Push Docker Image') {
			steps {
				script {
					docker.withRegistry('', 'dockerhub') {
					dockerImage.push()	
					dockerImage.push('latest')
					}
				}
			}
		}
	}
	post {
		always {
			echo 'i m awesome, i run always'
		}
		success {
			echo 'i run only when you are successful'
		}
		failure {
			echo 'i run only when you fail'
		}
	}
}
