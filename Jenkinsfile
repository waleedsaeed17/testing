pipeline {
    agent {label 'sys'}
    
    stages {
        
        stage('Show Changed Files') {
            steps {
                script {
                    def changedFiles = sh(script: 'git diff --name-only --diff-filter=AM HEAD@{1} HEAD', returnStdout: true).trim()
                    echo "Changed Files:"
                    echo changedFiles
                }
            }
        }
    }
}
