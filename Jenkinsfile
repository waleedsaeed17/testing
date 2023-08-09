pipeline {
    agent { label 'sys' }

    stages {
        stage('Find and Copy Modified/Added .properties files') {
            steps {
                script {
                    def modifiedFiles = bat(returnStdout: true, script: 'git diff --name-only --diff-filter=AM HEAD@{1} HEAD')
                    def propertiesFilesEvents = modifiedFiles.readLines().findAll { it.endsWith('.properties') }
                    def propertiesFilesAdmin = modifiedFiles.readLines().findAll { it.endsWith('.properties') }

                    if (propertiesFilesEvents || propertiesFilesAdmin) {
                        if (propertiesFilesEvents) {
                            propertiesFilesEvents.each { propertyFile ->
                                bat "xcopy /Y /I ${workspace}\\folder2\\${propertyFile} ${workspace}\\target_directory_events\\"
                            }
                        }
                        if (propertiesFilesAdmin) {
                            propertiesFilesAdmin.each { propertyFile ->
                                bat "xcopy /Y /I ${workspace}\\conf\\admin\\${propertyFile} ${workspace}\\target_directory_admin\\"
                            }
                        }
                    } else {
                        echo "No modified or added .properties files found."
                    }
                }
            }
        }
    }
}
