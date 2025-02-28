pipeline {
    agent any

    environment {
        GIT_REPO_URL = 'https://github.com/raysalfaa/assesment.git'
    }

    stages {
        stage('Check Branch') {
            steps {
                script {
                    // Correctly extract branch details
                    def targetBranch = env.CHANGE_TARGET ?: (env.BRANCH_NAME?.startsWith("PR-") ? null : env.BRANCH_NAME)
                    def sourceBranch = env.CHANGE_BRANCH ?: (env.GIT_BRANCH ?: env.BRANCH_NAME)

                    def cloneURL = env.GIT_URL ?: GIT_REPO_URL 
                    // echo "🚀 Target Branch: ${targetBranch}"
                    // echo "🚀 Source Branch: ${sourceBranch}"
                    // echo "🚀 Clone URL: ${cloneURL}"
                    

                    // Ensure targetBranch is detected
                    if (!targetBranch) {
                        error "❌ Target branch not detected! Webhook may not be configured properly."
                    }

                    // Skip build if target branch is prod or staging
                    if (targetBranch == 'prod' || targetBranch == 'staging') {
                        echo "⏩ Skipping build as target branch is ${targetBranch}"
                        currentBuild.result = 'ABORTED'
                        return
                    }

                    echo "🚀 Target Branch: ${targetBranch}"
                    echo "🚀 Source Branch: ${sourceBranch}"
                    echo "🚀 Clone URL: ${cloneURL}"
                }
            }
        }

        stage('Clone Repository') {
            steps {
                script {
                    def checkoutBranch = env.CHANGE_BRANCH ?: env.BRANCH_NAME
                    echo "🛠️ Checking out branch: ${checkoutBranch}"
                    git branch: "${checkoutBranch}", url: "${env.GIT_URL ?: GIT_REPO_URL}"
                }
            }
        }

        stage('Build') {
            steps {
                echo "🔧 Building project..."
            }
        }
    }

    post {
        always {
            echo "✅ Pipeline execution completed!"
        }
    }
}
