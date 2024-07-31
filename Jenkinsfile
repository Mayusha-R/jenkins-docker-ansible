pipeline {
    agent any
    stages {
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t mayusharathod/java-app:v2 .'
            }
        }
        stage('Push Docker Image') {
            steps {
		script {
                    docker.withRegistry('https://index.docker.io/v1/', "${env.DOCKER_ID}") {
                        docker.image('mayusharathod/java-app:v2').push('v2')
                    }
                }
            }
        }
        stage('Deploy Container') {
            steps {
                sh 'docker run -d -p 8089:8080 mayusharathod/java-app:v2'
            }
        }
    }
}
