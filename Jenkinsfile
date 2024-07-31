pipeline {
    agent any
    stages {
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t mayusharathod/java-app:v3 .'
            }
        }
        stage('Push Docker Image') {
            steps {
		script {
                    docker.withRegistry('https://index.docker.io/v1/', "${env.DOCKER_ID}") {
                        docker.image('mayusharathod/java-app:v3').push('v3')
                    }
                }
            }
        }
        stage('Deploy Container') {
            steps {
                sh 'docker run -d -p 8089:8080 mayusharathod/java-app:v3'
            }
        }
    }
}
