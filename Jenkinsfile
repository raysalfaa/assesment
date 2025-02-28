pipeline {
    agent any

    triggers {
        genericTrigger(
            genericVariables: [
                [key: 'ACTION', value: '$.action'],
                [key: 'BASE_BRANCH', value: '$.pull_request.base.ref'],
                [key: 'SOURCE_BRANCH', value: '$.pull_request.head.ref'],
                [key: 'CLONE_URL', value: '$.pull_request.head.repo.clone_url']
            ],
            token: 'your-webhook-secret',
            printContributedVariables: true,
            printPostContent: true
        )
    }

    stages {
        stage('Check Branch') {
            steps {
                script {
                    echo "Target Branch: ${env.BASE_BRANCH}"
                    echo "Source Branch: ${env.SOURCE_BRANCH}"
                    echo "Clone URL: ${env.CLONE_URL}"
                }
            }
        }

        stage('Clone Repository') {
            steps {
                script {
                    if (env.SOURCE_BRANCH == null || env.SOURCE_BRANCH == '') {
                        error "Source branch is missing. Ensure webhook is correctly configured."
                    }
                    git branch: "${env.SOURCE_BRANCH}", url: "${env.CLONE_URL}"
                }
            }
        }
    }
}
