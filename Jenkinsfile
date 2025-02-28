pipeline {
    agent any  // Runs on any available agent
 
    environment {
        SONARQUBE_URL = 'http://localhost:9000'  // Update if needed
    }
 
    stages {
        stage('Checkout') {
            steps {
                git branch: 'dev', url: 'https://github.com/raysalfaa/assesment.git'
            }
        }
 
        stage('SonarQube Analysis') {
            steps {
                script {
                    def scannerHome = tool 'sonarscanner'  // Ensure this is configured in Jenkins
 
                    withSonarQubeEnv('SonarQube_server') {  // Change this to match your Jenkins SonarQube config
                        withCredentials([string(credentialsId: 'sonar-token', variable: 'SONARQUBE_TOKEN')]) {  // Update with correct credentials ID
                            sh """
                                ${scannerHome}/bin/sonar-scanner \\
                                -Dsonar.projectKey=sample \\
                                -Dsonar.sources=. \\
                                -Dsonar.host.url=${SONARQUBE_URL} \\
                                -Dsonar.login=${SONARQUBE_TOKEN}
                            """
                        }
                    }
                }
            }
        }
 
        stage('Quality Gate') {
            steps {
                timeout(time: 5, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}
 pipeline {
    agent any

    environment {
        GIT_REPO_URL = 'https://github.com/your-username/your-repo.git'
    }

    stages {
        stage('Check Branch') {
            steps {
                script {
                    def targetBranch = env.CHANGE_TARGET
                    def sourceBranch = env.CHANGE_BRANCH
                    def cloneURL = env.GIT_URL ?: GIT_REPO_URL  // Clone URL from webhook or default

                    if (targetBranch == 'prod' || targetBranch == 'staging') {
                        echo "Skipping build as target branch is ${targetBranch}"
                        currentBuild.result = 'ABORTED'
                        return
                    }

                    echo "Target Branch: ${targetBranch}"
                    echo "Source Branch: ${sourceBranch}"
                    echo "Clone URL: ${cloneURL}"
                }
            }
        }

        stage('Clone Repository') {
            steps {
                git branch: "${env.CHANGE_BRANCH}", url: "${env.GIT_URL ?: GIT_REPO_URL}"
            }
        }

        stage('Build') {
            steps {
                echo "Building project..."
                // Add build commands here, like Maven or Gradle
            }
        }
    }

    post {
        always {
            echo "Pipeline execution completed!"
        }
    }
}
