pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                script {
                    if (env.CHANGE_ID) {  // Check if triggered by a PR
                        def sourceBranch = env.CHANGE_BRANCH   // PR Source Branch
                        def baseBranch = env.CHANGE_TARGET     // PR Target Branch
                        def cloneURL = env.GIT_URL             // Clone URL

                        echo "Pull Request detected!"
                        echo "Source Branch: ${sourceBranch}"
                        echo "Base Branch: ${baseBranch}"
                        echo "Clone URL: ${cloneURL}"

                        // Clone the repo
                        checkout scm
                    } else {
                        echo "Not triggered by a PR. Skipping."
                        // currentBuild.result = 'ABORTED'
                        // error("This build runs only on pull requests.")
                        def sourceBranch = env.CHANGE_BRANCH   // PR Source Branch
                        def baseBranch = env.CHANGE_TARGET     // PR Target Branch
                        def cloneURL = env.GIT_URL             // Clone URL

                        echo "Pull Request detected!"
                        echo "Source Branch: ${sourceBranch}"
                        echo "Base Branch: ${baseBranch}"
                        echo "Clone URL: ${cloneURL}"
                    }
                }
            }
        }
    }
}
