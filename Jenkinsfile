pipeline {
    agent any

    stages {

        stage('Show New Commits') {
            steps {
                // Run git command to show new commits of a file
                bat 'git log --oneline --follow C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\testing\\script.txt'
            }
        }
    }
}
