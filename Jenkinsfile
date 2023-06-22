pipeline {
    agent { label 'ServerVM ' }
    
    stages {
        stage('Clone Repository') {
            steps {
                bat 'git clone https://github.com/waleedsaeed17/testing.git'
            }
        }
        
        stage('Compare and Extract Changes') {
            steps {
                script {
                    // Define the file path
                    def filePath = 'D:\\Tools\\jenkins-agent\\workspace\\test\\script.txt'
                    
                    // Get the previous commit hash
                    def previousCommit = bat(script: 'git rev-parse HEAD~1', returnStdout: true).trim()
                    
                    // Pull the latest changes
                    bat 'git pull'
                    
                    // Get the current commit hash
                    def currentCommit = bat(script: 'git rev-parse HEAD', returnStdout: true).trim()
                    
                    // Compare the file versions
                    def diffOutput = bat(script: "git diff --no-prefix ${previousCommit} ${currentCommit} -- ${filePath}", returnStdout: true).trim()
                    
                    // Save the diff output to a file
                    writeFile file: 'changes.txt', text: diffOutput
                }
            }
        }
    }
}
