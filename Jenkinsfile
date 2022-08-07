pipeline {
    agent {
        docker {
            image 'docker:latest'
            
        }
    }

    stages {
        stage('Hello') {
            steps {
                sh 'docker build -t helloworld .'
            }
        }
    }
}
