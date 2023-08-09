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
                                def sourceFile = "${workspace}\\folder2\\${propertyFile}"
                                def targetFile = "${workspace}\\target_directory_events\\${propertyFile}"
                                bat "copy /Y ${sourceFile} ${targetFile}"
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
