pipeline {
    agent any
    stages {
        stage('Build & Deploy Staging (infra010)') {
            steps {
                sh 'docker rm -f samplerunning || true'
                sh 'bash ./sample-app.sh'
            }
        }
        stage('Deploy Production (dmz010)') {
            steps {
                sshagent(['dmz010-ssh']) {
                    sh 'docker save sampleapp | ssh -o StrictHostKeyChecking=no admin@192.0.2.10 "docker load && docker rm -f sampleapp_prod || true && docker run -d --name sampleapp_prod -p 8000:5050 sampleapp"'
                }
            }
        }
    }
}
