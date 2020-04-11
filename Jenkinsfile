// New script Declarative
pipeline {
	agent any
	environment{
	dockerHome = tool 'MyDocker'
	mavenHome = tool 'MyMaven'
	PATH ="$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages{
		stage('Build'){
			steps{
			sh 'docker version'
			sh 'mvn --version'
			echo "Build"
			echo "PATH - $PATH"
			echo "BUILD_NUMBER - $env.BUILD_NUMBER"
			echo "BUILD_ID - $env.BUILD_ID"
			echo "BUILD_ID - $env.BUILD_TAG"
			}
		}
		stage('Test'){
			steps{
			echo "Test"
			}
		}
		stage('Integration Test'){
			steps{
			echo "Integration Test"
			}
		}
		stage('Package'){
			steps{
			sh "mvn package -DskipTests"
			}
		}
		stage('Build docker image'){
			steps{
				//"docker build -t harshalbawale/jenkin-devops-microservices:$env.BUILD_TAG"
				script{
					//dockerImage =docker.build(harshalbawale/jenkin-devops-microservices:${env.BUILD_TAG}")
					dockerImage =docker.build(harshalbawale/jenkin-devops-microservices:0.0.1")
				}
			}
		}
		stage('push docker image'){
			stapes{
				scripts{
				docker.withRegistory('','DockerHub'){
						dockerImage.push()
						dockerImage.push('latest')
					}
				}
			}
		}
	}
}
	