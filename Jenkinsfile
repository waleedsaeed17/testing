pipeline {
    agent {label 'sys'}

    stages {

        stage('Find and Copy Modified/Added .properties files') {
            steps {
                script {
                    def modifiedFiles = bat(returnStdout: true, script: 'git diff --name-only --diff-filter=AM HEAD@{1} HEAD')
                    def folder1 = modifiedFiles.split("\\n").findAll { it.endsWith('.properties') }
                    def folder2 = modifiedFiles.split("\\n").findAll { it.endsWith('.properties') }

                    if (folder1 || folder2 || folder) {
                        if (folder1) {
                            // Copy the modified/added .properties files in 'events' to target directory
                            bat "xcopy /Y /I /E ${workspace}\\testing\\folder1\\*.properties D:\\target_directory_events\\folder1"
                        }
                        if (folder2) {
                            // Copy the modified/added .properties files in 'events' to target directory
                            bat "xcopy /Y /I /E ${workspace}\\testing\\folder2\\*.properties D:\\target_directory_events\\folder2"
                    } else {
                        echo "No modified or added .properties files found."
                    }
                }
            }
        }
    }
}
