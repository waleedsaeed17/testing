pipeline {
    agent any

    stages {

        stage('Show New Commits') {
            steps {
                script {
                    // Get the commit hashes for the file
                    def commitHashes = sh(
                        script: "git log --pretty=format:'%H' --follow C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\testing\\script.txt",
                        returnStdout: true
                    ).trim().split('\n')
                    
                    // Iterate over the commit hashes and show the code changes
                    for (def commitHash in commitHashes) {
                        echo "Commit: ${commitHash}"
                        sh "git show --stat --oneline ${commitHash} -- C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\testing\\script.txt"
                        echo "\n"
                    }
                }
            }
        }
    }
}
