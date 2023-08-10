pipeline {
    agent {label 'sys'}
    
    stages {
        
        stage('Copy Changed Files') {
            steps {
                script {
                    def changedFiles = bat(script: 'git diff --name-only --diff-filter=AM HEAD@{1} HEAD', returnStdout: true).trim()
                    //echo "Changed Files:"
                    //echo changedFiles
                    
                    // Iterate through each changed file and copy if it's in the specified directory
                    changedFiles.split('\n').each { filePath ->
                        def backslashPath = filePath.replaceAll('/', '\\\\')
                        echo "File Path: ${backslashPath}"
                        
                        // Check if the file path contains 'folder1\\conf'
                        if (backslashPath.contains('folder1\\conf')) {
                            // Copy the file to D:\northstar
                            bat "xcopy /Y ${backslashPath} D:\\northstar\\"
                        }
                    }
                }
            }
        }
    }
}
