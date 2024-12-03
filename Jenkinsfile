pipeline {
    agent any
    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/Dineshraj25/react-project.git' 
            }
        }
        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }
        stage('Build React App') {
            steps {
                bat 'npm run build'
            }
        }
        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'build\\**', fingerprint: true
            }
        }
    }
}
