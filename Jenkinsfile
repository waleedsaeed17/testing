pipeline {
    agent {
        label 'windows'
    }
    
    stages {
        stage('Compare Files') {
            steps {
                // Define the file paths to be compared
                def file1 = 'script.txt'
                def file2 = 'change.txt'
                
                // Define the path for WinMerge executable
                def winmergePath = 'C:\\Program Files\\WinMerge\\WinMergeU.exe'
                
                // Define the path for delta.txt file
                def deltaFile = 'C:\\delta.txt'
                
                // Run WinMerge to compare files and generate delta.txt
                bat "\"${winmergePath}\" /e /u /wl /wr /dl \"File1\" /dr \"File2\" \"${file1}\" \"${file2}\" \"${deltaFile}\""
            }
        }
    }
}
