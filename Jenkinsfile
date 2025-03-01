pipeline {
    agent any

    triggers {
        githubPush()  // Triggers the pipeline on GitHub push events (PR updates)
    }

    environment {
        BASE_BRANCH = "${env.CHANGE_TARGET}"  // Base branch of the PR
        CLONE_URL = "https://github.com/raysalfaa/assesment.git"
    }

    stages {
        stage('Check Branch') {
            steps {
                script {
                    echo "Target Branch: ${BASE_BRANCH}"
                    echo "Source Branch: ${env.CHANGE_BRANCH }"
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

    }
}
