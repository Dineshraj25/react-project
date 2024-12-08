pipeline {
    agent any

    environment {
        SONAR_HOST_URL = 'http://localhost:9000'
        SONAR_TOKEN = credentials('sonarQube-token') // Replace 'sonarQube-token' with your credential ID
        NETLIFY_AUTH = credentials('netlify-auth-token') // Replace 'netlify-auth-token' with your credential ID
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
        stage('Check Build Directory') {
            steps {
                bat 'dir build'
            }
        }
        stage('Deploy to Netlify') {
            steps {
                bat 'npx netlify deploy --dir build --prod --auth %NETLIFY_AUTH%'
            }
        }
    }
}
