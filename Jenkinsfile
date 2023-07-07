pipeline {
    agent {
        label 'sys'
    }
    stages {
        stage('Extract Changes') {
            steps {
                script {
                    def previousCommit = sh(returnStdout: true, script: 'git rev-parse HEAD^').trim()
                    def currentCommit = sh(returnStdout: true, script: 'git rev-parse HEAD').trim()
                    def changedFiles = sh(returnStdout: true, script: "git diff --name-only ${previousCommit} ${currentCommit}").trim().split('\n')
                    
                    // Specify the file you want to extract changes from
                    def targetFile = 'D:\\jenkins_agent\\workspace\\test'
                    
                    if (changedFiles.contains(targetFile)) {
                        // Extract the changes from the target file
                        def extractedChanges = sh(returnStdout: true, script: "git diff ${previousCommit} ${currentCommit} -- ${targetFile}")
                        echo "Extracted Changes:\n${extractedChanges}"
                        
                        // Further processing of extracted changes
                        // ...
                    } else {
                        echo "No changes found in ${targetFile}"
                    }
                }
            }
        }
    }
}
