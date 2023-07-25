pipeline {
    agent {label 'sys'}

    stages {
        stage('Git Diff') {
            steps {
                bat '''@echo off
                REM Change the path to your Git repository
                cd C:\\Users\\Waleed Saeed\\Desktop\\test\\testing

                REM Run the git diff command
                "C:\\Program Files\\Git\\git-bash.exe" git diff --name-only --diff-filter=M HEAD@{1} HEAD
                '''
            }
        }
    }
}
