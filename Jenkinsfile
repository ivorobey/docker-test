pipeline {
  agent {
    kubernetes {
      label 'dind'
      defaultContainer 'docker'
      yaml """
---
apiVersion: v1
kind: Pod
metadata:
  labels:
    app: jenkins
spec:
  containers:
    - name: docker
      image: docker:latest
      command:
        - /bin/cat
      tty: true
      volumeMounts:
        - name: dind-certs
          mountPath: /certs
      env:
        - name: DOCKER_TLS_CERTDIR
          value: /certs
        - name: DOCKER_CERT_PATH
          value: /certs
        - name: DOCKER_TLS_VERIFY
          value: 1
        - name: DOCKER_HOST
          value: tcp://localhost:2376
    - name: dind
      image: docker:dind
      securityContext:
        privileged: true
      env:
        - name: DOCKER_TLS_CERTDIR
          value: /certs
      volumeMounts:
        - name: dind-storage
          mountPath: /var/lib/docker
        - name: dind-certs
          mountPath: /certs/client
  volumes:
    - name: dind-storage
      emptyDir: {}
    - name: dind-certs
      emptyDir: {}
"""
    }
  }
  stages {
    stage('Run Docker Things') {
      steps {
        sh 'docker build -t local/hello-world .'
        sh 'docker run local/hello-world'
      }
    }
  }
}
