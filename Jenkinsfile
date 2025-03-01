pipeline {
    agent any
    environment {
        GIT_CREDENTIALS_ID = 'your-github-credentials-id'  // Replace with correct ID
        GIT_REPO = 'https://github.com/raysalfaa/assesment.git'
    }
    stages {
        stage('Checkout PR') {
            steps {
                script {
                    checkout([
                        $class: 'GitSCM',
                        branches: [[name: "*/PR-${env.CHANGE_ID}"]],
                        userRemoteConfigs: [[
                            url: env.GIT_REPO,
                            credentialsId: env.GIT_CREDENTIALS_ID
                        ]]
                    ])
                }
            }
        }
        stage('Build') {
            steps {
                echo 'Building PR...'
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
            }
        }
    }
}
