pipeline {
    agent {label 'sys'}

    stages {
        stage('Run Git Command') {
            steps {
                // Change to the workspace directory
                dir("${WORKSPACE}") {
                    // Run your Git commands here
                    // For example, if you want to list the files in the current workspace, you can use:
                    echo "MODIFIED FILES"
                    bat 'git diff --name-only --diff-filter=M HEAD@{1} HEAD'
                }
            }
        }
    }
}
