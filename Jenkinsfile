pipeline {
    agent {label 'sys'}
    
    stages {
        
        stage('Check for Changes') {
            steps {
                script {
                    // Get the list of changed files since the last build
                    def changedFiles = bat(returnStdout: true, script: 'git diff --name-only --diff-filter=AM HEAD@{1} HEAD')
                    
                    // Split the changed files into a list
                    def filesToCopy = changedFiles.trim().split('\n').findAll { it.startsWith('folder1\\conf\\') }
                    
                    // Copy the changed files to D:\northstar
                    filesToCopy.each { file ->
                        bat(script: "copy ${file.replace('\\', '\\\\')} D:\\\\northstar\\\\")
                    }
                }
            }
        }
    }
}
