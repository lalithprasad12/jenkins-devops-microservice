#!/bin/bash
//SCRIPTED
//node {
	//stage('Build') {
		//echo "Build"
	//}
	//stage('Test') {
		//echo "Test"
	//}
	//stage('Integration Test') {
		//echo "Test"
	//}
//}

//DECLARATIVE

pipeline{
		//agent any
		agent { docker { image 'node:7-alpine'} }
			stages {
				stage ('Build') {
					steps {
							//sh "mvn --version"
							echo "Build"
							}
					}
					stage ('Test') {
						steps {
								echo "Test"
									}
								}
						stage ('Integration Test') {
							steps {
									echo "Integration Test"
							}
				}
		 }
		 post {
		 		always {
					echo "I am awesome, I run always"
				}
				success {
					echo "I run when you are success"
				}
				failure {
					echo "I run when you fail"
				}
		 }
}
