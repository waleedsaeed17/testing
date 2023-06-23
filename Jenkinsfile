pipeline {
    agent {label 'ServerVM'}
    
    stages {
        stage('Compare Files') {
            steps {
                script {
                    // Set the paths to the files
                    def originalFile = "script.txt"
                    def modifiedFile = "change.txt"
                    def finalFile = "final.txt"
                    
                    // Read the contents of the original file
                    def originalContent = readFile file: originalFile
                    
                    // Read the contents of the modified file
                    def modifiedContent = readFile file: modifiedFile
                    
                    // Compare the files' data
                    def diffResult = diffFiles(originalContent, modifiedContent)
                    
                    // Create a new file to store the differences
                    def finalOutput = new File(finalFile)
                    
                    // Write the differences to the new file
                    finalOutput.write(diffResult)
                }
            }
        }
    }
}

def diffFiles(original, modified) {
    // Use a diff library or tool to compare the files' data and extract differences
    // Replace this with the appropriate diff library or command-line tool for your needs
    // Here's an example using the WinMerge command-line tool
    def diffCommand = "C:/Program Files/WinMerge/WinMergeU.exe /e /u /wl /wr /dl 'Original' /dr 'Modified' '${original}' '${modified}'"
    def diffResult = bat(returnStdout: true, script: diffCommand)
    
    // Return the differences
    return diffResult
}
