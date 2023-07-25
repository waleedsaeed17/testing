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

                        // Write modified file paths to the text file, one path per line
                        modifiedFiles.each { fileName ->
                            writeFile file: filePath, text: "${workspacePath}\\${fileName}\n", append: true
                        }

                        // Print the file path where the modified file paths are stored
                        echo "Modified file paths saved in: ${filePath}"
                    }
                }
            }
        }
    }
}
