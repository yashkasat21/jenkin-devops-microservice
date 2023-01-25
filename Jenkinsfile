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
		stage('Build') {
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
		stage('Test') {
			steps {
				echo "Test"
			}
		}
		stage('Integration Test') {
			steps {
				echo "Integration Test"
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
