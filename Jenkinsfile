pipeline {
    agent any
	stages {
		stage ('docker') {
			steps {
				sh 'docker build -t node .'
			}
		}
		stage ('run') {
			steps {
				sh 'docker run --rm node'
			}
		}
        stage('Build') {
            steps {
                sh 'npm install'
				echo 'this is build'
				echo 'test'
            }
        }
        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
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
