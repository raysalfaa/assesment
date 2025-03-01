pipeline {
    agent any
    triggers {
        githubPullRequest {
            orgWhitelist(['your-github-org'])  // Replace with your GitHub Org/User
            allowMembersOfWhitelistedOrgsAsAdmin(true)
            permitAll(true)
            cron('* * * * *')  // Polls GitHub every minute for PR changes
        }
    }
    stages {
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
}
