pipeline {
    agent {
        any {
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
        stage('Archive Artifact'){
            steps{
                sh 'npm pack | tail -n 1'
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: '**/movie-analyst-api-*.tgz', fingerprint: true
            junit '**/*.xml'
        }
    }
}