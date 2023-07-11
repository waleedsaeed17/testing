pipeline {
    agent any

    stages {

        stage('Fetch Data') {
            steps {
                script {
                    // Get the commit IDs of the specific file
                    def commitIds = sh(
                        script: 'git log --format="%H" -- D:/git/test.txt',
                        returnStdout: true
                    ).trim().split('\n')

                    // Iterate over the commit IDs and fetch the actual data
                    for (def commitId in commitIds) {
                        sh "git checkout ${commitId} -- D:/git/test.txt"
                        
                        // Display the commit ID and the actual data
                        echo "Commit ID: ${commitId}"
                        sh "type D:/git/test.txt"
                        echo "--------------------"
                    }
                }
            }
        }
    }
}
