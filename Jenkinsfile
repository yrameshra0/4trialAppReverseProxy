pipeline {
    agent any
    environment {
        SWARM_SERVICE_NAME = 'app_rev_proxy'
    }
    stages {
        stage('Build with unit testing') {
            steps {
                echo 'Pulling...' + env.BRANCH_NAME
                sh """
                docker build -t ${env.SWARM_SERVICE_NAME}:${env.GIT_COMMIT} .
                """
            }
        }  

        stage('Update TEST swarm') {
            steps {
                sh """
                docker service create \
                --publish 12000:80 \
                --replicas 1 \
                --name test_${SWARM_SERVICE_NAME} \
                --update-delay 10s \
                --network test \
                ${env.SWARM_SERVICE_NAME}:${env.GIT_COMMIT}
                """
            }
        }    

        stage('Update PROD swarm') {
            steps {
                sh """
                docker service create \
                --publish 11000:80 \
                --replicas 1 \
                --name test_${SWARM_SERVICE_NAME} \
                --update-delay 10s \
                --network prod \
                ${env.SWARM_SERVICE_NAME}:${env.GIT_COMMIT}
                """
            }
        }    
    }
}