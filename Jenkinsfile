pipeline {
  agent {
    kubernetes {
      yaml '''
        apiVersion: v1
        kind: Pod
        spec:
          containers:
          - name: docker
            image: docker:latest
            command:
            - cat
            tty: true
            volumeMounts:
             - mountPath: /var/run/docker.sock
               name: docker-sock
          volumes:
          - name: docker-sock
            hostPath:
              path: /var/run/docker.sock    
        '''
    }
  }
  stages {
    stage('Clone') {
      steps {
        container('docker') {
          git branch: 'main', changelog: false, poll: false, url: 'https://github.com/khalid244/test-registry.git'
        }
      }
    }  
    // stage('Build-Jar-file') {
    //   steps {
    //     container('maven') {
    //       sh 'mvn package'
    //     }
    //   }
    // }
    stage('Build-Docker-Image') {
      steps {
        container('docker') {
          sh 'docker build -t 8858764865/test-registry:latest .'
        }
      }
    }
    stage('Login-Into-Docker') {
      steps {
        container('docker') {
          sh 'docker login -u 8858764865 -p nijopa8266'
      }
    }
    }
     stage('Push-Images-Docker-to-DockerHub') {
      steps {
        container('docker') {
          sh 'docker push 8858764865/test-registry:latest'
      }
    }
     }
  }
    post {
      always {
        container('docker') {
          sh 'docker logout'
      }
      }
    }
}