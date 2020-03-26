pipeline {

    agent {
        dockerfile true
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
                sh 'chmod 400 DevopsDiegoKey.pem'
                sh 'scp -i "DevopsDiegoKey.pem" -o StrictHostKeyChecking=no movie-analyst-ui-*.tgz ubuntu@18.217.109.21:/home/ubuntu/'
                sh 'ssh -i "DevopsDiegoKey.pem" -o StrictHostKeyChecking=no ubuntu@18.217.109.21 tar -xvzf /home/ubuntu/movie-analyst-ui-1.0.0.tgz'
                sh 'ssh -i "DevopsDiegoKey.pem" -o StrictHostKeyChecking=no ubuntu@18.217.109.21 ls'
                sh 'ssh -i "DevopsDiegoKey.pem" -o StrictHostKeyChecking=no ubuntu@18.217.109.21 chmod +x  /home/ubuntu/package/script.sh'
                sh 'ssh -i "DevopsDiegoKey.pem" -o StrictHostKeyChecking=no ubuntu@18.217.109.21  /home/ubuntu/package/script.sh'
            }
        }       
    }
}
