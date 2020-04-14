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
                sh 'scp -i "DevopsDiegoKey.pem" -o StrictHostKeyChecking=no movie-analyst-ui-*.tgz ubuntu@3.15.184.150:/home/ubuntu/'
                sh 'ssh -i "DevopsDiegoKey.pem" -o StrictHostKeyChecking=no ubuntu@3.15.184.150 tar -xvzf /home/ubuntu/movie-analyst-ui-1.0.0.tgz'
                sh 'ssh -i "DevopsDiegoKey.pem" -o StrictHostKeyChecking=no ubuntu@3.15.184.150 ls'
                sh 'ssh -i "DevopsDiegoKey.pem" -o StrictHostKeyChecking=no ubuntu@3.15.184.150 ansible-playbook /home/ubuntu/package/mUI.yml'
            }
        }       
    }
}
