pipeline {
    agent {label 'sys'}

    stages {

        stage('Find and Copy Modified/Added .properties files') {
            steps {
                script {
                    def modifiedFiles = bat(returnStdout: true, script: 'git diff --name-only --diff-filter=AM HEAD@{1} HEAD')
                    def propertiesFilesEvents = modifiedFiles.split("\\n").findAll { it.endsWith('.properties') }
                    def propertiesFilesAdmin = modifiedFiles.split("\\n").findAll { it.endsWith('.properties') }

                    if (propertiesFilesEvents || propertiesFilesAdmin) {
                        if (propertiesFilesEvents) {
                            // Copy the modified/added .properties files in 'events' to target directory
                            bat "xcopy /Y /I /E ${workspace}\\folder2\\*.properties ${workspace}\\target_directory_events\\"
                        }
                        if (propertiesFilesAdmin) {
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
