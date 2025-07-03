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
    stage('Build DB Images'){
            steps {
              sh 'docker compose -f ${COMPOSE_FILE} build db' 
              sh 'docker compose -f ${COMPOSE_FILE} up -d db' 
              
            }

        }    
    
    stage('Build APP Images'){
            steps {
              sh 'docker compose -f ${COMPOSE_FILE} build server' 
              sh 'docker compose -f ${COMPOSE_FILE} build service1' 
              sh 'docker compose -f ${COMPOSE_FILE} build service2'               
            }
        }  
    stage('Docker App Container Start'){
            steps {
                sh 'docker compose -f ${COMPOSE_FILE} up -d' 

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

                        docker compose -f ${COMPOSE_FILE} push

                        rm -f ~/.docker/config.json


                    '''
                }
            }
        }       

       
    }
}