pipeline {
    agent any


    triggers {
        githubPush()  // Triggers the pipeline on GitHub push events (PR updates)
    }

    environment {
        BASE_BRANCH = "${env.GIT_BRANCH}"  // Base branch of the PR
        CLONE_URL = "https://github.com/raysalfaa/assesment.git"

    triggers {
        githubPullRequest {
            orgWhitelist(['your-github-org'])  // Replace with your GitHub Org/User
            allowMembersOfWhitelistedOrgsAsAdmin(true)
            permitAll(true)
            cron('* * * * *')  // Polls GitHub every minute for PR changes
        }
    }
    stages {

        stage('Check Branch') {
            steps {
                script {
                    echo "Target Branch: ${BASE_BRANCH}"
                    echo "Source Branch: ${GIT_BRANCH}"
                    echo "Clone URL: ${CLONE_URL}"
                }
            }
        }

        stage('Clone Repository') {
            steps {
                script {
                    git branch: "${GIT_BRANCH}", 
                    credentialsId: 'github1', 
                    url: "${CLONE_URL}"
                }
            }
        }
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                echo 'Building the PR...'
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying...'
            }
        
    }
}
