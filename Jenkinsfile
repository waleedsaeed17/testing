pipeline {
    agent any

    stages {

        stage('Fetch Data') {
            steps {
                script {
                    // Get the commit IDs
                    def commitIds = sh(
                        script: 'git log --format="%H"',
                        returnStdout: true
                    ).trim().split('\n')

                    // Iterate over the commit IDs and fetch the actual data
                    for (def commitId in commitIds) {
                        // Checkout the specific commit
                        sh "git checkout ${commitId}"
                        
                        // Display the commit ID and the actual data
                        echo "Commit ID: ${commitId}"
                        sh "D:\\git"
                        echo "--------------------"
                    }
                }
            }
        }
    }
}
