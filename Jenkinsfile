pipeline {
    agent any

    environment {
        SONARQUBE_URL = 'http://localhost:9000'   // Change if SonarQube is running on another server
        SONARQUBE_SCANNER = 'SonarScanner'  // Name in Global Tool Configuration
        SONARQUBE_TOKEN = credentials('sonar')  // Securely fetch token from Jenkins credentials
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/raysalfaa/assesment.git'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh """
                        ${SONARQUBE_SCANNER}/bin/sonar-scanner \
                        -Dsonar.projectKey=my-project \
                        -Dsonar.sources=. \
                        -Dsonar.host.url=${SONARQUBE_URL} \
                        -Dsonar.login=${SONARQUBE_TOKEN}
                    """
                }
            }
        }
    }

    post {
        always {
            echo "Pipeline execution completed!"
        }
    }
}
