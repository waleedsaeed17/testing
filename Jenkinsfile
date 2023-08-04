pipeline {
    agent {label 'sys'}

    stages {
        stage('Find and Copy Modified/Added .properties files') {
            steps {
                script {
                    def modifiedFiles = bat(returnStdout: true, script: 'git diff --name-only --diff-filter=MA origin/master...HEAD')
                    def folder1 = modifiedFiles.split("\\n").findAll { it.endsWith('.properties') }
                    def folder2 = modifiedFiles.split("\\n").findAll { it.endsWith('.properties') }

                    if (folder1 || folder2) {
                        if (folder1) {
                            // Copy the modified/added .properties files in 'events' to target directory
                            bat "xcopy /Y /I /E ${workspace}\\folder1\\*.properties D:\\target_directory_events\\folder1"
                        }
                        if (folder2) {
                            // Copy the modified/added .properties files in 'admin' to target directory
                            bat "xcopy /Y /I /E ${workspace}\\folder2\\*.properties D:\\target_directory_admin\\folder2"
                        }
                    } else {
                        echo "No modified or added .properties files found."
                    }
                }
            }
        }
    }
}
