pipeline {
  agent {
    kubernetes {
      label 'dind'
      defaultContainer 'docker'
    }
  }
  stages {
    stage('Run Docker Things') {
      steps {
        sh 'printenv'
        sh 'docker info'
      }
    }
  }
}
