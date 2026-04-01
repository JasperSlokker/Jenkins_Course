pipeline {
    agent {
        docker {
            image 'node:18-alpine'
            reuseNode true
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }

    environment {
        DOCKER_HOST = 'unix:///var/run/docker.sock'
    }

    stages {
        stage('Build'){
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
        stage('Test'){
            steps {
                echo "Test Stage"
                // Optioneel: als je ook echt de npm testen wilt draaien:
                dir('learn-jenkins-app') {
                    sh 'test -f build.index.html'
                }
            }
        }
    }
}