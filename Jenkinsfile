pipeline {
    agent { label 'sys' }

    stages {
        stage('Run Git Commands') {
            steps {
                // Change to the workspace directory
                dir("${WORKSPACE}") {
                    // Run the Git command and get the list of modified files
                    script {
                        def gitModified = bat(returnStdout: true, script: 'git diff --name-only --diff-filter=AM HEAD@{1} HEAD')
                        def modifiedFiles = gitModified.readLines()

                        // Write the modified files to a text file
                        with open('modified_files.txt', 'w') as f:
                            for file in modifiedFiles:
                                f.write(file + '\n')
                    }
                }
            }
        }
    }
}
