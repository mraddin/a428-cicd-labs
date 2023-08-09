pipeline {
    agent {
        docker {
            image 'node:16-buster-slim' 
            args '-p 3000:3000' 
        }
    }
    stages {
        stage('Build') { 
            steps {
                sh 'npm update'
                sh 'npm install' 
            }
        }
        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Manual Approval') {
            steps {
                    input message: 'Lanjutkan ke tahap Deploy?'
            }
        }
        stage('Deploy') {
             steps {
                sh './jenkins/scripts/deliver.sh'
                echo 'Waiting 1 minutes'
                sleep(time:60, unit:"SECONDS")
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}