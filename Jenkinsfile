pipeline {
    agent any
    stages {
        stage('Build') {
            agent {
                docker {
                    image 'ebogachev/dockerimage:latest'
                    registryCredentialsId 'dockerhub'
                    args '-v /var/run/docker.sock:/var/run/docker.sock -u root:root'
                    reuseNode true
                }
            }
            steps {
                git 'https://github.com/ebogachev/boxfuse.git'
                sh "mvn clean package"
            }
        }
    }
}
