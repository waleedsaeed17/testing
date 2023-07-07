pipeline {
    agent any
    
    stages {        
        stage('Extract Changes') {
            steps {
                script {
                    // Get the commit ID of the last successful build
                    def lastSuccessfulCommit = sh(returnStdout: true, script: 'git rev-parse HEAD').trim()
                    
                    // Get the commit ID of the latest commit
                    def latestCommit = sh(returnStdout: true, script: 'git rev-parse HEAD^').trim()
                    
                    // Get the changed files between the last successful commit and the latest commit
                    def changedFiles = sh(returnStdout: true, script: "git diff --name-only ${lastSuccessfulCommit} ${latestCommit}").trim().split('\n')
                    
                    // Extract changes for the specific file
                    def filePath = 'D:\\jenkins_agent\\workspace\\test\\sript.txt'
                    
                    if (changedFiles.contains(filePath)) {
                        sh "git show ${latestCommit}:${filePath} > extracted_changes.txt"
                    } else {
                        echo "No changes detected in ${filePath}"
                    }
                }
            }
        }
    }
}
