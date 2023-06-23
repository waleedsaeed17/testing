pipeline {
    agent {
        label 'ServerVM'
    }
    
    stages {
        stage('Compare Files') {
            steps {
                script {
                    // Path to the WinMerge executable
                    def winmergePath = "C:\\Program Files\\WinMerge\\WinMergeU.exe"
                    
                    // Path to the files to be compared
                    def file1 = "script.txt"
                    def file2 = "change.txt"
                    
                    // Path to the output text file
                    def outputFile = "final.txt"
                    
                    // Run WinMerge to compare the files
                    bat "\"${winmergePath}\" /r /e /s /u /wl /maximize \"${file1}\" \"${file2}\""
                    
                    // Read the output from WinMerge and extract unique data from the second file
                    def winmergeOutput = readFile(file: "${outputFile}", encoding: 'UTF-8')
                    def uniqueData = winmergeOutput.readLines().findAll { line -> line.startsWith("=>") }.collect { line -> line.substring(3) }
                    
                    // Write the unique data to a new text file
                    writeFile file: 'delta.txt', text: uniqueData.join('\n')
                }
            }
        }
    }
}
