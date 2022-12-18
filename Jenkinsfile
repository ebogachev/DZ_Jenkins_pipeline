pipeline {
    agent any
    stages {
        stage('Build and push') {
            agent {
                docker {
                    image 'ebogachev/dockerimage:latest'
                    registryCredentialsId 'dockerhub'
                    args '-v /var/run/docker.sock:/var/run/docker.sock -u root'
                    reuseNode true
                }
            }
            steps {
                git 'https://github.com/ebogachev/boxfuse.git'
                sh "mvn clean package"
                sh "echo FROM ebogachev/tomcat-image > Dockerfile"
                sh "echo COPY ./target/hello-1.0.war /opt/tomcat/webapps/hello-1.0.war >> Dockerfile"
                sh "docker build -t ebogachev/boxfuse ./"
                sh "docker push ebogachev/boxfuse"
            }
        }
        stage('Deploy on prod'){
            steps{
                
            }
        }
        
        
        
        
        
    }
}
