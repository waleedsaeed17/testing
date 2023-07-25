pipeline {
    agent { label 'sys' }

    stages {
        stage('Run Git Commands') {
            steps {
                // Change to the workspace directory
                dir("${WORKSPACE}") {
                    // Run the Git command and save the output to a file
                    script {
                        def gitDiffOutput = bat(returnStdout: true, script: 'git diff --name-only --diff-filter=AM HEAD@{1} HEAD')
                        writeFile file: 'git_diff_output.txt', text: gitDiffOutput
                    }
                }
            }
        }
    }

    post {
        always {
            // Archive the git_diff_output.txt file
            archiveArtifacts artifacts: 'git_diff_output.txt', onlyIfSuccessful: false
        }
    }
}
