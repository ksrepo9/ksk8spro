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

         stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh '''
                        # Login without persisting credentials
                        echo "$DOCKER_PASS" | docker login --username $DOCKER_USER --password-stdin
                    '''
                }
            }
        }       

        stage('Build Images'){
            steps {
              sh 'docker compose -f ${COMPOSE_FILE} build server' 
              
            }

        }
    }
}