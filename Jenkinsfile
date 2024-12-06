pipeline {
    agent any
    stages {
        stage('Build and run docker image') {
            steps {
                sh 'sudo docker pull divash10/devopsexam:latest'
                sh 'sudo docker run -d -p 8082:80 divash10/devopsexam:latest'
            } 
        }


        stage('testing') {
            steps {
                sh 'curl -I 20.151.77.171:8082'
            }
        }

    
    }
}
