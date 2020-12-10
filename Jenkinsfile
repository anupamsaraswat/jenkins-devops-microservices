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
			  sh "mvn package"
			  echo "mvn package"
			}
		}
		stage('Docker build'){
			steps{
				script{
				 dockerImage = docker.build("anupamsaraswat/currency-exchange-devops:${env.BUILD_TAG}")
				}
			}
		}
		stage('Docker Push'){
			steps{
				script{
					docker.withRegistry('', 'docker'){
						dockerImage.push();
						dockerImage.push('latest');
				    }
				}
			}
		}
	}
}
