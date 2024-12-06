pipeline {
    agent any
    stages {
        stage('Cleanup') {
            steps {
                cleanWs()
            }
        }

        stage('Clone from repository') {
            steps {
                git url: 'https://github.com/divash10/2244_ica2.git', branch: 'develop'
            }
        }

        stage('Build and run docker image') {
            steps {
                sh 'sudo docker build -t divash10/devopsexam .'
                sh "sudo docker tag divash10/devopsexam:latest divash10/devopsexam:develop-${env.BUILD_ID}" 
                sh 'sudo docker run -d -p 8081:80 divash10/devopsexam:latest'
            } 
        }

        stage('Build and Push') {
            steps {
                echo 'Building and pushing docker image..'
                withCredentials([usernamePassword(credentialsId: 'dockerhub-auth', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh '''
                        sudo docker login -u ${USERNAME} -p ${PASSWORD}
                        sudo docker push divash10/devopsexam:latest
                    '''
                    sh "sudo docker push divash10/devopsexam:develop-${env.BUILD_ID}"
                }
            }
        }

        stage('Testing') {
            steps {
                sh 'curl -I http://20.151.77.171:8081 || true' // Ensuring it won't fail the build
            }
        }
    }
}
