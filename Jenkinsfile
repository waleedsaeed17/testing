pipeline {
    agent {
        label 'windows'
    }
    
    environment {
        FILE_PATH = 'C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\testing\\script.txt' // Specify the file path here
    }
    
    stages {
        
        stage('Extract Commit IDs') {
            steps {
                script {
                    def commits = sh(script: "git log --pretty=format:\"%H\" -- ${env.FILE_PATH}", returnStdout: true).trim().split('\n')
                    env.COMMIT_IDS = commits.join(',')
                }
            }
        }
        
        stage('Checkout Code') {
            steps {
                script {
                    def commitIds = env.COMMIT_IDS.split(',')
                    for (int i = 0; i < commitIds.size(); i++) {
                        def commitId = commitIds[i]
                        echo "Checking out commit: ${commitId}"
                        
                        sh "git checkout ${commitId} -- ${env.FILE_PATH}"
                        
                        // Add additional steps to build/test the code against the commit
                        // For example:
                        // sh "mvn clean test"
                    }
                }
            }
        }
    }
}
