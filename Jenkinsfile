pipeline {
    agent any
    tools {
        // a bit ugly because there is no `@Symbol` annotation for the DockerTool
        // see the discussion about this in PR 77 and PR 52: 
        // https://github.com/jenkinsci/docker-commons-plugin/pull/77#discussion_r280910822
        // https://github.com/jenkinsci/docker-commons-plugin/pull/52
        'org.jenkinsci.plugins.docker.commons.tools.DockerTool' '18.09'
    }
    environment {
        DOCKER_TAG = getDockerTag()
        DOCKER_CERT_PATH = credentials('id-for-a-docker-cred')
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