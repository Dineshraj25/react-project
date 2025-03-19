pipeline {
    agent any

    environment {
        SONAR_HOST_URL = 'http://localhost:9000'
        SONAR_TOKEN = credentials('sonarQube-token') // SonarQube token
        NETLIFY_AUTH_TOKEN = credentials('netlify-auth-token') // Netlify authentication token
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
                bat """
                set NETLIFY_AUTH_TOKEN=%NETLIFY_AUTH_TOKEN%
                npx netlify link --id 557661fc-8743-4041-a2b0-3a792ea14e01
                npx netlify deploy --dir build --prod
                """
            }
        }
    }
}
