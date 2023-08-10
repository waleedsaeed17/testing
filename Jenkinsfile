pipeline {
    agent {label 'sys'}
    
    stages {
        
        stage('Check for Changes') {
            steps {
                script {
                    // Get the list of changed files since the last build
                    def changedFiles = bat(returnStatus: true, script: 'git diff --name-only HEAD^ HEAD')
                    
                    // Check if any changed file is in the 'folder1\conf' directory
                    def filesToCopy = changedFiles.tokenize('\n').findAll { it.startsWith('folder1\\conf\\') }
                    
                    // Copy the changed files to D:\northstar
                    filesToCopy.each { file ->
                        bat(script: "copy ${file.replace('\\', '\\\\')} D:\\\\northstar\\\\")
                    }
                }
            }
        }
    }
}
