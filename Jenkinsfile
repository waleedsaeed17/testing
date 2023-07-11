pipeline {
    parameters {
        string(name: 'filePath', defaultValue: 'C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\testing\\script.txt', description: 'Path to the file for diff')
    }
    agent any
    
    stages {
        stage('Sync and Diff') {
            steps {
                bat 'git pull' // Perform a git pull to synchronize the repository
                bat "C:\\Program Files\\WinMerge\\WinMergeU.exe C:\\Path\\To\\Previous\\Version\\script.txt C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\testing\\script.txt" // Use the correct path to WinMerge and specify the paths of the previous and current versions of the file
            }
        }
    }
}
