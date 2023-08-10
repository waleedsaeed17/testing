pipeline {
    agent {label 'sys'}

    stages {
        stage('Clone and Check') {
            steps {
                script {
                    // Get a list of modified or added files
                    def diffOutput = bat(script: 'git diff --name-status HEAD@{1} HEAD', returnStdout: true).trim()
                    def changedFiles = diffOutput.readLines().findAll { it.startsWith('M') || it.startsWith('A') }

                    // Copy changed files from folder1/conf to D:/northstar
                    echo "Changed files:"
                    for (file in changedFiles) {
                        echo file
                        if (file.contains('folder1/conf/')) {
                            def fileName = file.split()[1]
                            bat "copy workspace\\${fileName} D:\\northstar\\"
                        }
                    }
                }
            }
        }
    }
}
