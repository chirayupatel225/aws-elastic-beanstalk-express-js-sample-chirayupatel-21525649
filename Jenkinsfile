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
        stage('Snyk Security Scan') {
            steps {
                sh 'npm install -g snyk'
                script {
                    def result = sh(script: 'snyk test', returnStatus: true)
                    if (result != 0) {
                        error "Critical vulnerabilities found! Halting the pipeline."
                    }
                }
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
            echo 'Pipeline Finished.'
        }
    }
}
