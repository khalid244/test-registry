pipeline {
    agent any
    environment {
        DOCKER_TAG = getDockerTag()
    }
     stage('Initialize'){
        def dockerHome = tool 'Docker'
        env.PATH = "${dockerHome}/bin:${env.PATH}"
    }
    stages {
        stage('Build Docker Image') {
            steps {
                sh "docker build . -t 8858764865/test-registry:${DOCKER_TAG}"
            }
        }
    }
}

def getDockerTag() {
    def tag = sh script: 'git rev-parse HEAD', returnStdout: true
    return tag
}