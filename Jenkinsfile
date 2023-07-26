pipeline {
    agent { label 'sys' }

    stages {
        stage('Modified Files') {
            steps {
                // Change to the workspace directory
                dir("${WORKSPACE}") {
                    // Run the Git command and print the complete path of modified and new added files
                    script {
                        def gitModified = bat(returnStdout: true, script: 'git diff --name-only --diff-filter=AM HEAD@{1} HEAD')
                        def workspacePath = pwd() // Get the current workspace path
                        gitModified.readLines().each { fileName ->
                            echo "Modified/New Files: ${workspacePath}\\${fileName}"
                        }
                    }
                }
            }
        }
        
        stage('Deleted Files') {
            steps {
                // Change to the workspace directory
                dir("${WORKSPACE}") {
                    // Run the Git command and print the complete path of deleted files
                    script {
                        def gitDeleted = bat(returnStdout: true, script: 'git diff --name-only --diff-filter=D HEAD@{1} HEAD')
                        def workspacePath = pwd() // Get the current workspace path
                        gitDeleted.readLines().each { fileName ->
                            echo "Deleted Files: ${workspacePath}\\${fileName}"
                        }
                    }
                }
            }
        }
    }
}
