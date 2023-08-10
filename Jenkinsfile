pipeline {
    agent {
        label "sys" // Replace with the label of your Windows agent
    }
    
    stages {
        
        stage('Show Changed Files') {
            steps {
                script {
                    // Use PowerShell to get the list of changed files
                    def changedFiles = powershell(script: 'git diff --name-only HEAD^', returnStdout: true).trim()
                    
                    // Convert newline-separated string to list
                    def changedFilesList = changedFiles.split('\n')
                    
                    echo "Changed files:"
                    
                    // Print the changed files with full path
                    for (file in changedFilesList) {
                        def fullPath = powershell(script: "(Get-Item -Path ${file}).FullName", returnStdout: true).trim()
                        echo "${fullPath}"
                    }
                }
            }
        }
    }
}
