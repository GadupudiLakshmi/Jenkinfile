pipeline {
    agent none
	environment {
		CI = 'true'
	}
	stages {
		stage ('Build') {
			steps {
    			agent {
					docker { image 'node:14-alpine' }
				}
			}
		}
        stage('Test') {
            steps {
                sh 'node --version'
				echo 'hello'
            }
        }
        stage('Deliver for development') {
            when {
                branch 'development' 
            }
            steps {
                sh './jenkins/scripts/deliver-for-development.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }
        stage('Deploy for production') {
            when {
                branch 'production'  
            }
            steps {
                sh './jenkins/scripts/deploy-for-production.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}
