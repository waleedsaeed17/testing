pipeline {
    agent { label 'sys' }

    stages {
        stage('Run Git Commands') {
            steps {
                // Change to the workspace directory
                dir("${WORKSPACE}") {
                    // Run the Git command and save the modified file paths to a text file
                    script {
                        def gitModified = bat(returnStdout: true, script: 'git diff --name-only --diff-filter=AM HEAD@{1} HEAD')
                        def workspacePath = pwd() // Get the current workspace path
                        def modifiedFiles = gitModified.readLines().findAll { it !=~ /^D:/ } // Filter out unnecessary lines

                        def filePath = "${workspacePath}\\modified_files.txt" // File to store modified file paths

                        // Accumulate the modified file paths as a single string with each path on a new line
                        def modifiedFilesText = modifiedFiles.collect { "${workspacePath}\\${it}" }.join('\n')

                        // Write all modified file paths to the text file
                        writeFile file: filePath, text: modifiedFilesText

                        // Print the file path where the modified file paths are stored
                        echo "Modified file paths saved in: ${filePath}"
                    }
                }
            }
        }
    }
}
