pipeline {
    agent {
	   label 'docker'
	}
	environment {
		COMPOSE_FILE = 'compose.yaml'
        DOCKER_REGISTRY = 'kartikeyasoft'
        DOCKERHUB_CREDENTIALS = credentials('dockerhub')
	}

    stages {
        stage('Code Checkout') {
            steps {
             git branch: 'main', credentialsId: 'git', url: 'https://github.com/ksrepo9/ksk8spro.git'

            }
        }
        stage('Build Images'){
            steps {
               sh 'ls -l'
              
            }

        }
    }
}