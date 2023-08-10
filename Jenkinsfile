pipeline {
    agent {label 'sys'}
    
    stages {
        
        stage('Show Changed Files') {
            steps {
                script {
                    def changedFiles = bat(script: 'git diff --name-only --diff-filter=AM HEAD@{1} HEAD', returnStdout: true).trim()
                    //echo "Changed Files:"
                    //echo changedFiles
                    
                    // Iterate through each changed file and print its path with backslashes
                    changedFiles.split('\n').each { filePath ->
                        def backslashPath = filePath.replaceAll('/', '\\')
                        echo "File Path: ${backslashPath}"
                        
                        // Check if the file path matches the condition
                        if (backslashPath == 'folder1\\conf\\') {
                            // Copy the file to D:\northstar
                            bat "copy ${backslashPath} D:\\northstar"
                        }
                    }
                }
            }
        }
    }
}
