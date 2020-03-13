pipeline {

    agent {
        docker { image 'node:10-alpine' }
    }

    stages {
        
        stage('Install dependencies Stage') { 
            steps {
                sh 'npm install'
            }
        }

        stage('Archive Artifact'){
            steps{
                sh 'npm pack | tail -n 1'
                archiveArtifacts artifacts: '**/movie-analyst-ui-*.tgz', fingerprint: true
            }
        }       
    }
}
