pipeline{
    agent {
        docker { 
			image 'node:16.0' 
			label 'ci-cd'
		}
    }
    
 stages{
        stage('Build'){
            steps{
                echo 'Building app...'
				dir('/var/jenkins_home/workspace/devOpsLab07'){
					sh 'docker-compose  build  build-agent'
				}
            }  
            post{
				failure{
					emailext attachLog: true,
						body: "${currentBuild.currentResult}: ${currentBuild.fullDisplayName}",
                        to: 'simonconbrio@gmail.com',
                        subject: "Jenkins build failed ${env.BUILD_NUMBER}"
				}
				success{
					emailext attachLog: true,
						body: "${currentBuild.currentResult}: ${currentBuild.fullDisplayName}",
                        to: 'simonconbrio@gmail.com',
                        subject: "Jenkins build succeed ${env.BUILD_NUMBER}"
				}
			}   
        } 
        stage('Test'){
            steps{
                echo 'Testing app...'
                sh 'docker-compose  build  test-agent' 
            }
            post{
				failure{
					emailext attachLog: true,
						body: "${currentBuild.currentResult}: ${currentBuild.fullDisplayName}",
                        to: 'simonconbrio@gmail.com',
                        subject: "Jenkins test failed ${env.BUILD_NUMBER}"
				}
				success{
					emailext attachLog: true,
						body: "${currentBuild.currentResult}: ${currentBuild.fullDisplayName}",
                        to: 'simonconbrio@gmail.com',
                        subject: "Jenkins test succeed ${env.BUILD_NUMBER}"
				}
			}
        }
		
        stage('Deploy'){
			steps{
				echo 'Deploying...'
				sh 'docker-compose  up -d build-agent'
			}
			post{
				failure{
					emailext attachLog: true,
						body: "${currentBuild.currentResult}: ${currentBuild.fullDisplayName}",
                        to: 'simonconbrio@gmail.com',
                        subject: "Jenkins deploy failed ${env.BUILD_NUMBER}"
				}
				success{
					emailext attachLog: true,
						body: "${currentBuild.currentResult}: ${currentBuild.fullDisplayName}",
                        to: 'simonconbrio@gmail.com',
                        subject: "Jenkins deploy succeed ${env.BUILD_NUMBER}"
				}
			}
        }		
        }  
 }