pipeline {
    agent {label 'sys'}
    
    stages {
        stage('Detect and Process Changes') {
            steps {
                script {
                    // Define a variable to hold the list of changed files
                    def changedFiles = bat(script: 'git diff --name-only --diff-filter=AM HEAD@{1} HEAD', returnStdout: true).trim()

                    echo "Changed Files:"
                    echo changedFiles

                    // Iterate through each changed file and find related files in the specified directory
                    changedFiles.split('\n').each { filePath ->
                        def backslashPath = filePath.replaceAll('/', '\\\\')
                        echo "File Path: ${backslashPath}"
                        
                        // Check if the changed file is in the src/build directory and has a .java extension
                        if (backslashPath =~ /^src\\build\\.*\.java$/) {
                            def fileName = backslashPath.replaceAll('.*/(.*\\.java)', '$1')
                            echo "Detected Java File: ${fileName}"
                            
                            // Construct the source and destination paths
                            def sourcePath = "D:\\northstar\\WEB-INF\\classes\\${fileName}"
                            def destinationPath = "D:\\myfiles\\${fileName}"
                            
                            // Copy the file from source to destination
                            bat "xcopy /Y \"${sourcePath}\" \"${destinationPath}\""
                            echo "Copied ${fileName} to ${destinationPath}"
                        }
                    }
                }
            }
        }
    }
}
