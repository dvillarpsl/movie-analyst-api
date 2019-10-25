pipeline {
    agent { dockerfile true }
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