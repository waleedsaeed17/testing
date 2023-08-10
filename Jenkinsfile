pipeline {
    agent {label 'sys'}
    
    stages {
        
        stage('Pull and Copy') {
            steps {
                script {
                    // Get the list of added and modified files in the specified directory
                    def changedFiles = bat(script: 'git diff --name-only --diff-filter=AM HEAD@{1} HEAD folder1/conf', returnStdout: true).trim()
                    
                    // Copy changed files to the destination folder if any
                    if (!changedFiles.isEmpty()) {
                        def destinationFolder = 'D:\\northstar'
                        
                        // Create the destination folder if it doesn't exist
                        bat "mkdir ${destinationFolder}"
                        
                        // Copy changed files to the destination folder
                        changedFiles.split('\r\n').each { file ->
                            bat "copy \"${file}\" \"${destinationFolder}\""
                        }
                        
                        echo "Copied changed files to ${destinationFolder}"
                    } else {
                        echo "No changed files found in conf/admin directory."
                    }
                }
            }
        }
    }
}
