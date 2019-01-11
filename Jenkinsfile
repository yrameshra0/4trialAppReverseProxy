pipeline {
    agent any
    environment {
        SWARM_SERVICE_NAME = 'stack_proxy'
    }
    stages {
        stage('Build with unit testing') {
            steps {
                sh """docker build -t ${env.SWARM_SERVICE_NAME}:${env.GIT_COMMIT} ."""
            }
        }  

        stage('Update TEST swarm') {
            steps {
                sh """
                docker service update \
                --publish-add published=12001,target=80 \
                --replicas 1 \
                --update-delay 10s \
                --image ${env.SWARM_SERVICE_NAME}:${env.GIT_COMMIT} \
                test_${env.SWARM_SERVICE_NAME}
                """
            }
        }    

        stage('Update PROD swarm') {
            steps {
                sh """
                docker service update \
                --publish-add published=11001,target=80 \
                --replicas 1 \
                --update-delay 10s \
                --image ${env.SWARM_SERVICE_NAME}:${env.GIT_COMMIT} \
                prod_${env.SWARM_SERVICE_NAME}
                """
            }
        }    
    }
}
