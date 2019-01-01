pipeline {
    agent { any }
    environment {
        SWARM_SERVICE_NAME = 'app_rev_proxy'
    }
    stages {
        stage('Build with unit testing') {
            step {
                echo 'Pulling...' + env.BRANCH_NAME
                docker build -t app_rev_proxy .
        }
    } 
}