pipeline {
    agent any

    stages {
        stage('Compare changes') {
            steps {
                script {
                    // Define the paths of the file to compare
                    def fileToCompare = 'C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\now\\script.txt'
                    def outputFile = 'D:\\file.txt'

                    // Run WinMerge to compare the file with its current version
                    bat "\"C:\\Program Files\\WinMerge\" /e /u /wl /wr /dl \"Current Version\" /dr \"New Changes\" /ub /nb /minimize /x /maximize /s /f1 \"${fileToCompare}\" /f2 . /fo=\"${outputFile}\""

                    // Print the output file path
                    echo "Output file: ${outputFile}"
                }
            }
        }
    }
}
