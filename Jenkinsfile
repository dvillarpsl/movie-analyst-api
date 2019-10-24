pipeline {
    agent {
        docker {
            image 'node:6-alpine' 
            args '-p 3000:3000' 
        }
    }
    stages {
        stage('Build') { 
            steps {
                sh 'npm install'
            }
        }
        stage('Test'){
            steps{
                sh 'npm test'
            }
        }
    }
    post {
        always {
            junit '*/test-results.xml'
        }
        success {
            steps {
                sh 'npm pack | tail -n 1'
            }
        }
    }
}