pipeline {
    agent { label 'ServerVM ' } 

    stages {
        stage('Compare Files') {
            steps {
                // Clone the Git repository
                checkout scm

                // Define the file paths
                def oldFilePath = '‪D:\\Tools\\jenkins-agent\\workspace\\test\\change.txt'
                def newFilePath = '‪D:\\Tools\\jenkins-agent\\workspace\\test\\script.txt'
                def changesFilePath = 'path/to/changes/file'

                // Compare the files and extract changes
                bat "git diff --no-renames --unified=0 ${oldFilePath} ${newFilePath} > ${changesFilePath}"

                // Display the changes
                bat "type ${changesFilePath}"
            }
        }
    }
}
