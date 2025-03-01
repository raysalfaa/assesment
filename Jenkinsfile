// pipeline {
//     agent any
//     stages {
//         stage('Checkout') {
//             steps {
//                 script {
//                     def branchName = env.GIT_BRANCH
//                     def sourceBranch = env.CHANGE_BRANCH  // Source branch
//                     def baseBranch = env.CHANGE_TARGET   // Base branch

//                     if (env.CHANGE_ID) {
//                         echo "Pull Request Detected!"
//                         echo "Source Branch: ${sourceBranch}"
//                         echo "Base Branch: ${baseBranch}"
//                     } else {
//                         echo "Regular Build - Branch: ${branchName}"

//                         echo" ${baseBranch}"
//                     }
//                 }
//             }
//         }
//     }
// }

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

