pipeline {
    agent any
    stages {
        stage('Job1 - Build') {
            steps {
                sh 'docker build -t myapp:latest .'
            }
        }
        stage('Job2 - Test') {
            steps {
                sh 'docker run --rm myapp:latest echo "Test Passed!"'
            }
        }
        stage('Job3 - Prod') {
            when {
                branch 'master'
            }
            steps {
                sh 'docker stop prod || true'
                sh 'docker rm prod || true'
                sh 'docker run -d --name prod -p 80:80 myapp:latest'
            }
        }
    }
}
