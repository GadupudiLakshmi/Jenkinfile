pipeline {
    agent {
		docker {
			image 'node:14-alpine'
		}
	}
	environment {
		CI = 'true'
	}
	stages {
		stage ('Build') {
			steps {
				echo 'installed'
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
				echo 'deliver success'
            }
        }
        stage('Deploy for production') {
            when {
                branch 'production'  
            }
            steps {
				echo 'production success'
            }

        }
    }
}
