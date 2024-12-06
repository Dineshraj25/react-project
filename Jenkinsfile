pipeline {
    agent any

    tools {
        nodejs 'NodeJS' // Make sure to configure NodeJS in Jenkins Global Tool Configuration
    }

    environment {
        SONAR_HOST_URL = 'http://localhost:9000' // Adjust the URL if needed
        SONAR_TOKEN = credentials('sonarQube-token') // Replace 'sonarqube-token' with your actual Jenkins credential ID
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
                withSonarQubeEnv('SonarQube') { // 'SonarQube' matches the name in Jenkins SonarQube server configuration
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
