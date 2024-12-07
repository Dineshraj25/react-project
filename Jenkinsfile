pipeline {
    agent any

    environment {
        SONAR_HOST_URL = 'http://localhost:9000'
        SONAR_TOKEN = credentials('sonarQube-token') // Replace with your credential ID
    }

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
        stage('Install Netlify CLI') {
            steps {
                bat 'npm install -g netlify-cli'
            }
        }
        stage('Deploy to Netlify') {
            steps {
                bat 'netlify deploy --dir build --prod --auth <your-auth-token>'
            }
        }
    }
}
