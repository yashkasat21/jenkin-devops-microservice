//DECLARATIVE

pipeline {
	//agent any
	agent { docker { image: 'maven:3.6.3'}}
	stages {
		stage('Build') {
			steps {
				echo "Build"
				sh 'mvn --version'
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
