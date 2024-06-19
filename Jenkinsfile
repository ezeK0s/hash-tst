pipeline {
    agent {
        label 'agent-node'
    }
    
    environment {
        dkcr_ape = credentials('ape1-8088')
    }
    
    stages {
        stage('Clone the repository') {
            steps {
                git branch: 'main', url: 'https://github.com/ezeK0s/hash-tst.git'
            }
        }   
        stage('dependencied, build') {
            steps {
                sh '''
                npm install
                npm run build
                '''
            }
        }
        stage('docker'){
            steps {
                sh '''
                docker login -u apezekos -p $dkcr_ape
                docker build . -t apezekos/hash-git
                docker push apezekos/hash-git:latest
                '''
            }
        }
    }
}