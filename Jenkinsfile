pipeline {
    agent any
    stages {
        stage('Build project') {
            agent {
                docker {
                    image 'ebogachev/dockerimage:latest'
                    args '-v /var/run/docker.sock:/var/run/docker.sock -u root'
                    reuseNode true
                }
            }
            steps {
                git 'https://github.com/ebogachev/boxfuse.git'
                sh "mvn clean package"
            }
        }
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
                sh "mkdir /usr/local/tomcat"
                sh "mkdir /usr/local/tomcat/webapps"
                sh "cp ./target/hello-1.0.war /usr/local/tomcat/webapps/hello-1.0.war"
                sh "docker build -t ebogachev/boxfuse ./"
                sh "docker push ebogachev/boxfuse"
            }
        }
        stage('Deploy on prod'){
            steps{
                sshagent(credentials: ['9fe5a7ca-caf4-4a7b-84b7-a1d136596a24']) {
                 sh 'ssh -o StrictHostKeyChecking=no -l root 158.160.4.156'
                 sh   "docker pull ebogachev/boxfuse"
                 sh   "docker run -p 80:8080 -d ebogachev/boxfuse"  
                }
            }
        }
        
    }
}
