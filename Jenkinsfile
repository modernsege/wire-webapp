pipeline{
    agent {
        docker { image 'node:16.0' }
    }
    
 stages{
        stage('Build'){
            steps{
                echo 'Building app...'
                sh 'yarn install'
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
                sh 'yarn test:server' 
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
				sh 'docker build -t deploy -f Dockerfile /deploy-dockerfile/'
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