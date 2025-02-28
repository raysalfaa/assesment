pipeline {
    agent any

    environment {
        GIT_REPO_URL = 'https://github.com/raysalfaa/assesment.git'
    }

    stages {
        stage('Check Branch') {
            steps {
                script {
                    def targetBranch = env.CHANGE_TARGET ?: env.BRANCH_NAME
                    def sourceBranch = env.CHANGE_BRANCH ?: env.GIT_BRANCH
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
                git branch: "${env.BRANCH_NAME}", url: "${env.GIT_URL ?: GIT_REPO_URL}"
            }
        }

        stage('Build') {
            steps {
                echo "Building project..."
            }
        }
    }

    post {
        always {
            echo "Pipeline execution completed!"
        }
    }
}
