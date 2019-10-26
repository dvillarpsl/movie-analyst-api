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
                archiveArtifacts artifacts: '**/movie-analyst-api-*.tgz', fingerprint: true
            }
        }
        stage ('Deploying Artifact') {
            steps {
                generatedTarFile = sh script: 'ls movie-analyst-api-*.tgz', returnStdout: true
                build job: 'deploy-movie-analyst-api', parameters: [
                string(name: 'artifactName', value: generatedTarFile),
                string(name: 'jobName', value: "movie-analyst-api"),
                string(name: 'buildNumber', value: "${currentBuild.number}")
                ]
            }
        }
    }
    post {
        always {
            junit '**/*.xml'
        }
    }
}