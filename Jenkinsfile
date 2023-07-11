pipeline {
    agent any
    
    stages {
        
        stage('Retrieve new commits') {
            steps {
                script {
                    // Assuming you want to track changes in a file named 'my_file.txt'
                    def fileToTrack = 'C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\testing\\script.txt'
                    
                    // Get the commit hash of the last successful build
                    def lastSuccessfulCommit = sh(
                        script: 'git rev-parse HEAD',
                        returnStdout: true
                    ).trim()
                    
                    // Get the commit hash of the latest commit in the repository
                    def latestCommit = sh(
                        script: 'git ls-remote origin HEAD',
                        returnStdout: true
                    ).trim().split()[0]
                    
                    // Retrieve the list of commits between the last successful build and the latest commit
                    def commitList = sh(
                        script: "git log --pretty=format:'%H' ${lastSuccessfulCommit}..${latestCommit} -- ${fileToTrack}",
                        returnStdout: true
                    ).trim().split('\n')
                    
                    // Process each commit
                    for (def commit in commitList) {
                        // Do whatever you want with each commit (e.g., notify, build, etc.)
                        echo "New commit: ${commit}"
                    }
                }
            }
        }
        
        // Add more stages for further actions based on the new commits
    }
}
