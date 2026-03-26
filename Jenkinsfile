pipeline {
    agent any

    environment {
        // Dit dwingt Jenkins om de Unix socket op je Mac/Container te gebruiken
        // in plaats van te zoeken naar een netwerk-host genaamd 'docker'
        DOCKER_HOST = 'unix:///var/run/docker.sock'
    }

    stages {
        stage('Build'){
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                    // We geven de socket door zodat de node-container ook 'docker' kan praten indien nodig
                    args '-v /var/run/docker.sock:/var/run/docker.sock'
                }
            }
            steps {
                dir('learn-jenkins-app') {
                    sh '''
                        node --version
                        npm --version
                        npm ci
                        npm run build
                    '''
                }
            }
        }
    }
}