pipeline {
	agent { docker { image 'maven:3.6.3'}}
	environment{
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	} 
	stages{
		stage('compile') {
			steps{
			  sh "mvn clean compile"
			  echo "Build"
			}
		}
		stage('Test') {
			steps{
			  echo "mvn test"
			}
		}
		stage('Package') {
			steps{
			  echo "mvn package"
			}
		}
		stage('Docker build'){
			script{
				dockerImage = docker.build("anupamsaraswat/currency-exchange-devops:${env.BUILD_TAG}")
			}
		}
		stage('Docker Push'){
			script{
				docker.withRegistry('', 'docker'){
					dockerImage.push();
					dockerImage.push('latest');
				}
			}
		}
	}
}
