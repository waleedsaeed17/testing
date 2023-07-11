pipeline {
    
    agent any
    
    stages {
        stage('Prepare') {
            steps {
                script {
                    def latestCommitHash = sh(script: "git log -1 --format=%H", returnStdout: true).trim()
                
                // Get the list of new commits
                    def newCommits = sh(script: "git log ${latestCommitHash}..HEAD --oneline", returnStdout: true).split('\n')

                // Get the path to the specific file
                    def filePath = 'C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\testing\\script.txt'

                // Get the list of new commits that affected the specific file
                    def affectedCommits = newCommits.findAll { it.contains(filePath) }

                // Print the list of new commits
                    echo "New commits: ${affectedCommits}"
                }
            }
        }
    }
}
