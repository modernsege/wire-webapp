pipeline{
    agent {
        docker { image 'node:16.0' }
    }
    
    stages{
        stage('Test'){
            steps{
                echo 'Testing app...'
				sh 'yarn install'
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

    }
 }