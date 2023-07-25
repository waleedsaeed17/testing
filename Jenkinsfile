pipeline {
    agent { label 'sys' }

    stages {
        stage('Run Git Commands') {
            steps {
                // Change to the workspace directory
                dir("${WORKSPACE}") {
                    // Run the Git command and save the modified file paths to a text file
                    script {
                        // Execute the Git command in a Windows shell using bat
                        def gitModified = bat(returnStdout: true, script: 'git diff --name-only --diff-filter=AM HEAD@{1} HEAD')
                        def workspacePath = pwd() // Get the current workspace path

                        // Split the output into lines and filter out unnecessary data
                        def modifiedFiles = gitModified.readLines().findAll { it !=~ /^D:/ }

                        def filePath = "${workspacePath}\\modified_files.txt" // File to store modified file paths

                        // Write all modified file paths to the text file
                        writeFile file: filePath, text: modifiedFiles.join('\n')

                        // Print the file path where the modified file paths are stored
                        echo "Modified file paths saved in: ${filePath}"
                    }
                }
            }
        }
    }
}
