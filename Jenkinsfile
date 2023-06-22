pipeline {
    
    agent { label 'ServerVM ' }

stages{
        stage('Stopping Tomcat svc'){
            steps {
                script {
                    // Define the file path and commit references
                    def filePath = 'D:\\Tools\\jenkins-agent\\workspace\\test\\script.txt'
                    def previousCommit = bat(script: 'git rev-parse HEAD~1', returnStdout: true).trim()
                    def currentCommit = bat(script: 'git rev-parse HEAD', returnStdout: true).trim()
                    
                    // Compare the file versions
                    def diffOutput = bat(script: 'git diff --no-prefix ${previousCommit} ${currentCommit} -- ${filePath}', returnStdout: true).trim()
                    
                    // Save the diff output to a file
                    writeFile file: 'changes.txt', text: diffOutput
                }

            }

        }

    }
}
