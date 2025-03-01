pipeline {
    agent any

    environment {
        TARGET_BRANCH = "${env.CHANGE_TARGET}" // Gets the target branch of the PR
    }

    stages {
        stage('Check Target Branch') {
            when {
                expression { 
                    return TARGET_BRANCH == "dev" 
                }
            }
            steps {
                echo "Target branch is 'dev', proceeding with the build."
                // Add your build steps here
            }
        }
    }

    post {
        always {
            echo "Pipeline execution completed."
        }
        success {
            echo "Build successful!"
        }
        failure {
            echo "Build failed!"
        }
    }
}
