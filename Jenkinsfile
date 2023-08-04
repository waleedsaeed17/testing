pipeline {
    agent {label 'sys'}

    stages {

        stage('Find and Copy Modified/Added .properties files') {
            steps {
                script {
                    def modifiedFiles = bat(returnStdout: true, script: 'git diff --name-only --diff-filter=AM HEAD@{1} HEAD')
                    def events = modifiedFiles.split("\\n").findAll { it.endsWith('.properties') }
                    def tes = modifiedFiles.split("\\n").findAll { it.endsWith('.properties') }

                    if (tes || admin || folder) {
                        if (tes) {
                            // Copy the modified/added .properties files in 'events' to target directory
                            bat "xcopy /Y /I /E ${workspace}\\tes\\*.properties ${workspace}\\target_directory_events\\"
                        }
                    } else {
                        echo "No modified or added .properties files found."
                    }
                }
            }
        }
    }
}
