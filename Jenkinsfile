pipeline {
    agent {
        docker {
            image 'node:16'
            args '-u root'
        }
    }
    stages {
        stage('Install Dependencies') {
            steps {
                sh 'npm install --save'
            }
        }
        stage('Run Tests') {
            steps {
                sh 'npm test'
            }
        }
    }
    post {
        always {
            echo 'Pipeline finished.'
        }
    }
}

