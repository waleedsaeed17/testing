pipeline {
    agent {label 'ServerVM'}
    
    stages {
        stage('Prepare Workspace') {
            steps {
                // Create a workspace directory
                bat 'mkdir workspace'
                
                // Copy the files to be compared to the workspace directory
                bat 'copy "script.txt" workspace\\script.txt'
                bat 'copy "change.txt" workspace\\change.txt'
            }
        }
        
        stage('Compare Files') {
            steps {
                // Run WinMerge to compare the files
                bat 'winmergeu.exe /r /e /u /wl "workspace\\script.txt" "workspace\\change.txt"'
            }
        }
        
        stage('Capture Changes') {
            steps {
                // Copy the changed data to another file
                bat 'echo. > workspace\\final.txt'
                bat 'winmergeu.exe /s "workspace\\script.txt" "workspace\\change.txt" /r /e /u /wl /minimize /maximize /dl "Base" /dr "Mine" /lefttitle "Original" /righttitle "Modified" /mergeoutput "workspace\\final.txt"'
            }
        }
    }
}
