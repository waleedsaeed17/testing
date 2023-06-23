pipeline {
    agent {label 'ServerVM'}

    stages {
        stage('Compare Files') {
            steps {
                script {
                    // Define the file paths
                    def file1Path = 'script.txt'
                    def file2Path = 'change.txt'
                    def finalFilePath = 'final.txt'

                    // Run WinMerge to compare the files
                    bat "\"C:\\Program Files\\WinMerge\\WinMergeU.exe\" /e /u /wl /maximize \"${file1Path}\" \"${file2Path}\""

                    // Save the WinMerge output to a file
                    bat "echo ^>^>^> WinMerge ^>^>^> ${finalFilePath}"
                    bat "echo. >> ${finalFilePath}"
                    bat "type WinMerge.log >> ${finalFilePath}"

                    // Print the content of the final file
                    bat "type ${finalFilePath}"
                }
            }
        }
    }
}
