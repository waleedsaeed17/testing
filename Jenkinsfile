pipeline {
    agent {label 'sys'}
    
    stages {
        
        stage('Show Changed Files') {
            steps {
                script {
                    def changedFiles = bat(script: 'git diff --name-only --diff-filter=AM HEAD@{1} HEAD', returnStdout: true).trim()
                    echo "Changed Files:"
                    echo changedFiles
                    
                    // Iterate through each changed file and print its path
                    changedFiles.split('\n').each { filePath ->
                        echo "File Path: ${filePath}"
                    }
                }
            }
        }
    }
}
