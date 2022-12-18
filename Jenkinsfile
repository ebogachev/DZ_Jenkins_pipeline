pipeline {
    agent any
    stages {
    stage('Fetch and maven build') {
  agent {
    docker {
        image 'node:16.13.1-alpine'
    }
  }

            steps {
                git 'https://github.com/ebogachev/boxfuse.git'
                sh "mvn package"
            }
  }
}
}
