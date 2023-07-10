pipeline {
    agent any

    stages {
        stage('Extract Changes') {
            steps {
                script {
                    // Get the previous build number
                    def previousBuildNumber = currentBuild.previousBuild()?.getNumber() ?: 0

                    // Determine the file to extract changes from
                    def filePath = 'D:\\jenkins_agent\\workspace\\testing\\script.txt'

                    // Get the changed files since the previous build
                    def changedFiles = sh(script: "git diff --name-only ${previousBuildNumber} HEAD | findstr ${filePath}", returnStdout: true).trim()

                    // Extract the changes
                    if (changedFiles) {
                        sh "git archive --format=zip --output=changes.zip HEAD $(git diff --name-only ${previousBuildNumber} HEAD ${changedFiles})"
                        archiveArtifacts artifacts: 'changes.zip', fingerprint: true
                    } else {
                        echo "No changes found in ${filePath}"
                    }
                }
            }
        }
    }
}
