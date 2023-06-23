pipeline {
    agent {
        label 'ServerVM'
    }
    stages {
        stage('Extract Commits') {
            steps {
                script {
                    def fileToCheck = 'script.txt' // Update with the actual path to your file
                    
                    def changelog = bat(
                        script: "git log --oneline --follow ${fileToCheck}",
                        returnStdout: true
                    ).trim()
                    
                    echo "Changelog for ${fileToCheck}:"
                    echo changelog
                }
            }
        }
    }
}
