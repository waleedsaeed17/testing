pipeline {
    agent {
        label 'ServerVM'
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Extract Commits') {
            steps {
                script {
                    def fileToCheck = 'script.txt' // Update with the actual path to your file
                    def outputFile = 'change.txt' // Update with the desired output file name
                    def referenceCommit = 'origin/master' // Update with the desired reference commit
                    
                    def changelog = bat(
                        script: "git log --format=format:\"%h %s%n%b\" ${referenceCommit}..HEAD --follow ${fileToCheck}",
                        returnStdout: true
                    ).trim()
                    
                    writeFile file: outputFile, text: changelog
                    
                    echo "Changelog for new commits of ${fileToCheck} has been written to ${outputFile}"
                }
            }
        }
    }
}
