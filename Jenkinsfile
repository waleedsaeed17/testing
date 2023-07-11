pipeline {
    agent any
    
    stages {
        
        stage('Get New Commits') {
            steps {
                script {
                    def fileToCheck = 'C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\testing\\script.txt'  // Specify the path to your file here
                    
                    def previousCommit = ""
                    def currentCommit = ""
                    
                    // Retrieve the previous commit from a saved file, if it exists
                    if (fileExists('previous_commit.txt')) {
                        previousCommit = readFile('previous_commit.txt').trim()
                    }
                    
                    // Get the current commit for the specified file
                    currentCommit = sh(
                        script: "git log -n 1 --format=format:'%H' -- '${fileToCheck}'",
                        returnStdout: true
                    ).trim()
                    
                    // Save the current commit for future use
                    writeFile file: 'previous_commit.txt', text: currentCommit
                    
                    // Get the new commits since the previous commit
                    def newCommits = sh(
                        script: "git log --pretty=format:'%H' ${previousCommit}..${currentCommit} -- '${fileToCheck}'",
                        returnStdout: true
                    ).trim()
                    
                    echo "New Commits:"
                    echo newCommits
                }
            }
        }
    }
    
    post {
        always {
            deleteFile 'previous_commit.txt'  // Clean up the saved commit file
        }
    }
}
