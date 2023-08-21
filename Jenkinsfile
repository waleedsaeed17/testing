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

                    }
                }
            }
        }
    }
}
