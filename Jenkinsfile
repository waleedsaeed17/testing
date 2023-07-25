pipeline {
    agent { label 'sys' }

    stages {
        stage('Run Git Commands - Modified and New Added Files') {
            steps {
                // Change to the workspace directory
                dir("${WORKSPACE}") {
                    // Run the Git command and print the complete path of modified and new added files
                    script {
                        def gitDiffOutput = bat(returnStdout: true, script: 'git diff --name-only --diff-filter=AM HEAD@{1} HEAD')
                        def workspacePath = pwd() // Get the current workspace path
                        gitDiffOutput.readLines().each { fileName ->
                            echo "Modified/New Added: ${workspacePath}\\${fileName}"
                        }
                    }
                }
            }
        }
        
        stage('Run Git Commands - Deleted Files') {
            steps {
                // Change to the workspace directory
                dir("${WORKSPACE}") {
                    // Run the Git command and print the complete path of deleted files
                    script {
                        def gitDiffDeletedOutput = bat(returnStdout: true, script: 'git diff --name-only --diff-filter=D HEAD@{1} HEAD')
                        def workspacePath = pwd() // Get the current workspace path
                        def deletedFilesPath = gitDiffDeletedOutput.readLines().collect { "${workspacePath}\\${it}" }.join('\n')
                        echo "Deleted:\n${deletedFilesPath}"
                        writeFile file: 'deleted_files.txt', text: deletedFilesPath
                    }
                }
            }
        }
    }
}
