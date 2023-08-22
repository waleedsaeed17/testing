pipeline {
    agent {label 'ui'}
    
    stages {
        
        stage('List and Process Changed Files') {
            steps {
                // Define the command to run Git diff and capture the output
                script {
                    def changedFiles = bat(script: 'git diff --name-only --diff-filter=AM HEAD@{1} HEAD', returnStdout: true).trim()
                    
                    echo "Changed Files:"
                    echo changedFiles
                    
                    // Iterate through each changed file and process them
                    changedFiles.split('\n').each { filePath ->
                        def backslashPath = filePath.replaceAll('/', '\\\\')
                        echo "File Path: ${backslashPath}"
                        
                        // Check if the file is in the specified directory and has a ".java" extension
                        if (backslashPath.contains("src\\build") && backslashPath.endsWith(".java")) {
                            // Extract the file name without extension
                            def fileName = backslashPath.substring(backslashPath.lastIndexOf('\\') + 1, backslashPath.lastIndexOf('.'))
                            
                            // Search for files in D:\northstar\WEB-INF\classes with the same name
                            def searchPattern = "D:\\northstar\\WEB-INF\\classes\\${fileName}*"
                            
                            // Copy matching files to D:\myfiles
                            bat "xcopy /Y /I \"${searchPattern}\" \"D:\\myfiles\\\""
                            
                            echo "Copied files with '${fileName}' prefix to D:\\myfiles\\"
                        }
                    }
                }
            }
        }
    }
    
}
