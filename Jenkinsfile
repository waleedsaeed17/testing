pipeline {
    agent {labe 'sys'}

    stages {

        stage('Run Git Commands') {
            steps {
                // Change to the workspace directory
                dir("${WORKSPACE}") {
                    // Run the Git command with echo for the heading
                    echo "=== Modified and New Added Files ==="
                    bat 'git diff --name-only --diff-filter=AM HEAD@{1} HEAD'
                }
            }
        }
    }
}
