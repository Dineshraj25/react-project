pipeline {
    agent any

    tools {
        nodejs 'NodeJS' // Replace with your configured NodeJS installation name
    }

    environment {
        SONAR_HOST_URL = 'http://localhost:9000'
        SONAR_TOKEN = credentials('sonarQube-token') // Replace 'sonarqube-token' with your credential ID
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
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') { // Ensure 'SonarQube' matches the Jenkins SonarQube configuration name
                    bat '''
                    sonar-scanner.bat \
                      -Dsonar.projectKey=react-project \
                      -Dsonar.sources=src \
                      -Dsonar.host.url=%SONAR_HOST_URL% \
                      -Dsonar.login=%SONAR_TOKEN%
                    '''
                }
            }
        }
        stage('Quality Gate') {
            steps {
                script {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'build\\**', fingerprint: true
            }
        }
    }
}
