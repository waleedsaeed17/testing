pipeline {
    agent any

    stages {

        stage('Find and Copy Modified/Added .properties files') {
            steps {
                script {
                    def modifiedFiles = bat(returnStdout: true, script: 'git diff --name-only --diff-filter=AM HEAD@{1} HEAD')
                    def events = modifiedFiles.split("\\n").findAll { it.endsWith('.properties') }
                    def tes = modifiedFiles.split("\\n").findAll { it.endsWith('.properties') }

                    if (events || admin || tes) {
                        if (tes) {
                            // Copy the modified/added .properties files in 'events' to target directory
                            bat "xcopy /Y /I /E ${workspace}\\tes\\*.properties ${workspace}\\target_directory_events\\"
                        }
                        if (admin) {
                            // Copy the modified/added .properties files in 'admin' to target directory
                            bat "xcopy /Y /I /E ${workspace}\\conf\\admin\\*.properties ${workspace}\\target_directory_admin\\"
                        }
                    } else {
                        echo "No modified or added .properties files found."
                    }
                }
            }
        }
    }
}
