pipeline {
    agent any

    stages {

        stage('Find and Copy Modified/Added .properties files') {
            steps {
                script {
                    def modifiedFiles = bat(returnStdout: true, script: 'git diff --name-only --diff-filter=AM HEAD@{1} HEAD')
                    def events = modifiedFiles.split("\\n").findAll { it.endsWith('.properties') }
                    def folder = modifiedFiles.split("\\n").findAll { it.endsWith('.properties') }

                    if (events || admin || folder) {
                        if (folder) {
                            // Copy the modified/added .properties files in 'events' to target directory
                            bat "xcopy /Y /I /E ${workspace}\\folder\\*.properties ${workspace}\\target_directory_events\\"
                        }
                    } else {
                        echo "No modified or added .properties files found."
                    }
                }
            }
        }
    }
}
