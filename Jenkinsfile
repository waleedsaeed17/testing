pipeline {
    agent {
        label 'ServerVM'
    }
    stages {
        stage('Extract Commits') {
            steps {
                script {
                    def fileToCheck = 'script.txt' // Update with the actual path to your file
                    def outputFile = 'change.txt' // Update with the desired output file name
                    
                    // Retrieve the latest commit hash for the specified file
                    def latestCommit = bat(
                        script: "git log -n 1 --format=format:%H --follow ${fileToCheck}",
                        returnStdout: true
                    ).trim()
                    
                    // Retrieve the commit details for the latest commit of the specified file
                    def changelog = bat(
                        script: "git log --format=format:\"%h %s%n%b\" ${latestCommit} --follow ${fileToCheck}",
                        returnStdout: true
                    ).trim()
                    
                    writeFile file: outputFile, text: changelog
                    
                    echo "Changelog for new commits of ${fileToCheck} has been written to ${outputFile}"
                }
            }
        }
    }
}
