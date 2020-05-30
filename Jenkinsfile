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
//---------------------------------------------------------------------------------------------------------------------
//DECLARATIVE

//pipeline{
		//agent any
		//agent { docker { image 'node:7-alpine'} }
			//stages {
				//stage ('Build') {
					//steps {
							//sh "mvn --version"
							//echo "Build"
							//}
					//}
					//stage ('Test') {
						//steps {
								//echo "Test"
									//}
								//}
						//stage ('Integration Test') {
							//steps {
									//echo "Integration Test"
							//}
				//}
		 //}
		 //post {
		 		//always {
					//echo "I am awesome, I run always"
				//}
				//success {
					//echo "I run when you are success"
				//}
				//failure {
					//echo "I run when you fail"
				//}
		 //}
//}

//---------------------------------------------------------------------------------------------------------------------

pipeline{
	
	agent any
	environment {
		dockerHome = tool 'DOCKER_HOME'
		mavenHome = tool 'MVN_HOME'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	
	stages {
		stage ('Checkout') {
			steps {
				sh 'mvn --version'
				sh 'docker version'
				echo "Build"
				echo "PATH - $PATH"
				echo "BUILD_NUMBER - $env.BUILD_NUMBER"
				echo "BUILD_ID - $env.BUILD_ID"
				echo "JOB_NAME - $env.JOB_NAME"
				echo "BUILD_TAG - $env.BUILD_TAG"
				echo "BUILD_URL - $env.BUILD_URL"
				
				}
			}
		
		stage ('Complie') {
			steps {
				sh 'mvn clean compile'
				}
			}
		
		stage ('Test') {
			steps {
				sh 'mvn test'
				}
			}
		
		stage ('Integration Test') {
			steps {
				sh 'mvn failsafe:integration-test failsafe:verify'
				}
			}
		
		stage ('Build Docker Image') {
			steps {
				//docker build -t lalithprasad12/hello-world-python:$env.BUILD_TAG This is a primitive way of doing things
				script {
					dockerImage = docker.build("lalithprasad12/currency-exchange-devops:${env.BUILD_TAG}")
					}
				}
			}
		
		stage ('Push Docker Image') {
			steps {
				script {
					dockerImage.push();
					dockerImage.push('latest')
					}
				
				}
			}
		
	}
	

}
