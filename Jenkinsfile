pipeline {
    agent {label 'sys'}

    stages {

        stage('List and Copy Files') {
            steps {
                script {
                    // Define source and target directories
                    def sourceDirectories = ['source_dir_1', '${worspace}\\folder1\\conf'] // Add your source directories here
                    def targetDirectories = ['target_dir_1', 'D:\\northstar'] // Add your target directories here
                    
                    
                    // Iterate over source directories
                    for (int i = 0; i < sourceDirectories.size(); i++) {
                        def sourceDir = sourceDirectories[i]
                        def targetDir = targetDirectories[i]
                        
                        // List new and modified files
                        def diffOutput = bat(script: "git diff --name-only --diff-filter=AM HEAD@{1} HEAD ${sourceDir}", returnStdout: true).trim()
                        def filesToCopy = diffOutput.readLines()
                        
                        // Copy files to target directory
                        for (String fileToCopy : filesToCopy) {
                            bat "robocopy ${sourceDir} ${targetDir} ${fileToCopy}"
                        }
                    }
                }
            }
        }
    }
}
