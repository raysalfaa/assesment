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
        PR_ACTION = ""
        SOURCE_BRANCH = ""
        BASE_BRANCH = ""
    }
    stages {
        stage('Extract PR Info') {
            steps {
                script {
                    def payload = readJSON text: env.GITHUB_EVENT_PAYLOAD
                    PR_ACTION = payload.action  // Example: "opened", "synchronize"
                    SOURCE_BRANCH = payload.pull_request.head.ref
                    BASE_BRANCH = payload.pull_request.base.ref
                    
                    echo "🔹 PR Action: ${PR_ACTION}"
                    echo "🔹 PR Source Branch: ${SOURCE_BRANCH}"
                    echo "🔹 PR Base Branch: ${BASE_BRANCH}"
                }
            }
        }
    }
}
