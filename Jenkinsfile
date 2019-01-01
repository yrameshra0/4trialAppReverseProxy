pipeline {
    agent { any }
    environment {
        SWARM_SERVICE_NAME = 'app_rev_proxy'
    }
    stages {
        stage('Build with unit testing') {
            step {
                echo 'Pulling...' + env.BRANCH_NAME
                docker build -t app_rev_proxy:env.BUILD_NUMBER} .
            }
            step {
                echo 'Verifying docker swarm service...' + env.SWARM_SERVICE_NAME
                if docker service ls --format "{{.Name}}" | grep -q env.BUILD_NUMBER
                then 
                    echo "SERVICE ALREADY CREATED | OK";
                else
                    echo "SERVICE NOT CREATED OK | NOT OK";
                fi
            }
        }
    } 
}