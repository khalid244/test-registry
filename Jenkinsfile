podTemplate(yaml: """
apiVersion: v1
kind: Pod
spec:
  containers:
  - name: docker
    image: docker:latest
    command: ['cat']
    tty: true
    volumeMounts:
    - name: dockersock
      mountPath: /var/run/docker.sock
  volumes:
  - name: dockersock
    hostPath:
      path: /var/run/docker.sock
"""
  ) {

  def image = "8858764865/test-registry"
  node(POD_LABEL) {
    stage('Clone github project') {
        git branch: 'main', url: 'https://github.com/khalid244/test-registry.git'
    }
    stage('Build docker image') {
      container('docker') {
        sh "docker build -t ${image} ."
      }
    }
    stage('Push docker image') {
      container('docker') {
        sh 'docker login -u 8858764865 -p nijopa8266'
        sh "docker push ${image}"
        sh 'docker logout'
      }
    }
  }
}


// podTemplate(yaml: """
// apiVersion: v1
// kind: Pod
// spec:
//   containers:
//   - name: docker
//     image: docker:latest
//     command: ['cat']
//     tty: true
//     volumeMounts:
//     - name: dockersock
//       mountPath: /var/run/docker.sock
//   volumes:
//   - name: dockersock
//     hostPath:
//       path: /var/run/docker.sock
// """
//   ) {

//   def image = "8858764865/test-registry"
//   node(POD_LABEL) {
//     stage('Build Docker image') {
//         git branch: 'main', url: 'https://github.com/khalid244/test-registry.git'
//       container('docker') {
//         sh "docker build -t ${image} ."
//         sh 'docker login -u 8858764865 -p nijopa8266'
//         sh "docker push ${image}"
//         sh 'docker logout'
//       }
//     }
//   }
// }



// podTemplate(containers: [
//     containerTemplate(name: 'docker', image: 'docker:latest', command: 'sleep', args: '99d'),
//   ]) {

//     node(POD_LABEL) {
//         container('docker') {
//             git branch: 'main', url: 'https://github.com/khalid244/test-registry'
//             // git branch: 'main', credentialsId: 'GithubCred', url: 'https://github.com/khalid244/test-registry'
//             stage('Get a Docker project') {
//                 sh 'docker build . -t 8858764865/test-registry'
//                 sh 'docker login -u 8858764865 -p nijopa8266'
//                 sh 'docker push 8858764865/test-registry'
//                 sh 'docker logout'
//             }
//         }
//     }
// }


// pipeline {
//   agent {
//     kubernetes {
//       yaml '''
//         apiVersion: v1
//         kind: Pod
//         spec:
//           containers:
//           - name: docker
//             image: docker:latest
//             command:
//             - cat
//             tty: true
//             volumeMounts:
//              - mountPath: /var/run/docker.sock
//                name: docker-sock
//           volumes:
//           - name: docker-sock
//             hostPath:
//               path: /var/run/docker.sock    
//         '''
//     }
//   }
//   stages {
//     stage('Clone') {
//       steps {
//         container('docker') {
//           git branch: 'main', changelog: false, poll: false, url: 'https://github.com/khalid244/test-registry.git'
//         }
//       }
//     }  
//     // stage('Build-Jar-file') {
//     //   steps {
//     //     container('maven') {
//     //       sh 'mvn package'
//     //     }
//     //   }
//     // }
//     stage('Build-Docker-Image') {
//       steps {
//         container('docker') {
//           sh 'docker build -t 8858764865/test-registry:latest .'
//         }
//       }
//     }
//     stage('Login-Into-Docker') {
//       steps {
//         container('docker') {
//           sh 'docker login -u 8858764865 -p nijopa8266'
//       }
//     }
//     }
//      stage('Push-Images-Docker-to-DockerHub') {
//       steps {
//         container('docker') {
//           sh 'docker push 8858764865/test-registry:latest'
//       }
//     }
//      }
//   }
//     post {
//       always {
//         container('docker') {
//           sh 'docker logout'
//       }
//       }
//     }
// }





// pipeline {
//     environment {
//         registry = "mcncyo/code-server"
//         registryCredential = 'dockerhub'
//     }
//     agent any
//     stages {
//         stage('Building image') {
//             steps{
//                 script {
//                     docker.build registry + ":$BUILD_NUMBER"
//                 }
//             }
//         }
//         stage('Publish') {
//             when {
//                 branch 'master'
//             }
//             steps {
//                 withDockerRegistry([ credentialsId: dockerhub, url: "" ]) {
//                     sh 'docker push mcncyo/code-server:latest'
//                 }
//             }
//         }
//     }
// }

