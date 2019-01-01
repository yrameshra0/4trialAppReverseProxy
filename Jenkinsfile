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
    }
}