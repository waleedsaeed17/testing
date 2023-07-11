pipeline {
    agent any

    stages {
        stage('Show New Commits') {
            steps {
                script {
                    // Get the commit hashes for the file
                    def commitHashes = bat(
                        script: 'git log --pretty=format:"%H" --follow -- C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\testing\\script.txt',
                        returnStdout: true
                    ).trim().split('\r\n')
                    
                    // Iterate over the commit hashes and show the code changes
                    for (def commitHash in commitHashes) {
                        echo "Commit: ${commitHash}"
                        bat "git show --stat --oneline ${commitHash} -- C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\testing\\script.txt"
                        echo "\n"
                    }
                }
            }
        }
    }
}
