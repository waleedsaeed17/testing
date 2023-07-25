pipeline {
    agent { label 'sys' }

    stages {
        stage('Run Git Commands') {
            steps {
                // Change to the workspace directory
                dir("${WORKSPACE}") {
                    // Run the Git command and print the complete path of files
                    script {
                        def gitDiffOutput = bat(returnStdout: true, script: 'git diff --name-only --diff-filter=AM HEAD@{1} HEAD')
                        def workspacePath = pwd() // Get the current workspace path
                        gitDiffOutput.readLines().each { fileName ->
                            echo "${workspacePath}\\${fileName}"
                        }
                    }
                }
            }
        }
    }
}
