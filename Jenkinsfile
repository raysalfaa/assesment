pipeline {
    agent any

    environment {
        SONARQUBE_URL = 'http://<SONARQUBE_IP>:9000'   // Change to your SonarQube server IP
        SONARQUBE_SCANNER = 'SonarScanner'  // The name given in Global Tool Configuration
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/raysalfaa/assesment.git'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {  // SonarQube name configured in Jenkins
                    sh '''
                        ${SONARQUBE_SCANNER}/bin/sonar-scanner \
                        -Dsonar.projectKey=my-project \
                        -Dsonar.sources=. \
                        -Dsonar.host.url=${SONARQUBE_URL} \
                        -Dsonar.login=<SONARQUBE_TOKEN>  // Replace with the token from SonarQube
                    '''
                }
            }
        }

        stage('Build') {
            steps {
                echo "Building the project..."
            }
        }

        stage('Quality Gate Check') {
            steps {
                script {
                    def qg = waitForQualityGate()
                    if (qg.status != 'OK') {
                        error "❌ Quality Gate failed: ${qg.status}"
                    }
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
