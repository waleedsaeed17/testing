pipeline {
    agent {label 'sys'}

    stages {
        stage('Pull and Copy Modified Files') {
            steps {
                // Pull updates from the remote repository
              
                // Get the list of modified files
                def modifiedFiles = bat (script: 'git diff --name-only --diff-filter=M HEAD@{1} HEAD', returnStdout: true).trim()

                // Create the destination directory (if needed)
                //bat 'mkdir C:\\path\\to\\destination_directory'

                // Copy the modified files to the destination directory
                bat "echo ${modifiedFiles} | xargs -I{} copy \"{}\" D:\\Release"
            }
        }
    }
}
