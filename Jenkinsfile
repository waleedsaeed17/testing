pipeline {
    agent {label 'sys'}

    stages {
        stage('Pull and Copy Modified Files') {
            steps {
                // Pull updates from the remote repository
                //sh 'git pull'

                // Get the list of modified files
                def modifiedFiles = sh script: 'git diff --name-only --diff-filter=M HEAD@{1} HEAD', returnStdout: true

                // Create a script block to process the output
                script {
                    // Split the output by newline to get a list of modified files
                    def modifiedFilesList = modifiedFiles.trim().split('\n')

                    // Create the destination directory (if needed)
                    //sh 'mkdir -p C:/path/to/destination_directory'

                    // Copy the modified files to the destination directory
                    modifiedFilesList.each { file ->
                        sh "copy ${file} D:\\Release"
                    }
                }
            }
        }
    }
}
