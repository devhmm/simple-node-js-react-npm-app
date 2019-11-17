pipeline {
    agent {
        docker {
            image 'node:10.16.3'
            args '-p 3000:3000'
        }
    }
    environment {
        CI = 'true'
        HOME="."
    }
    stages {
        stage('Check Environment') {
            steps {
                sh 'id'
                sh 'npm -v'
            }
        }
        stage('Build') {
            steps {
                sh '/usr/local/bin/npm install'
            }
        }
        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}