pipeline {
    agent {
        label 'ServerVM'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the source code
                checkout scm
            }
        }

        stage('Retrieve Latest Commit') {
            steps {
                // Get the latest commit ID and message for the file
                script {
                    def latestCommit = bat(returnStdout: true, script: "git log -n 1 --format=format:'%H' -- script.txt").trim()
                    def latestCommitMessage = bat(returnStdout: true, script: "git log -n 1 --format=format:'%s' -- script.txt").trim()
                    
                    // Write the commit data to a file
                    writeFile file: 'change.txt', text: "Latest Commit: ${latestCommit}\nMessage: ${latestCommitMessage}"
                }
            }
        }
    }
}
