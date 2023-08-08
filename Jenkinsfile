pipeline {
    agent any

    stages {
        stage('Find and Copy Modified .properties Files') {
            steps {
                script {
                    // Get the list of modified or added .properties files since the last pull
                    def modifiedFilesEvents = bat(returnStdout: true, script: 'git diff --name-only --diff-filter=AM HEAD@{1} HEAD')
                    def propertiesFiles = modifiedFilesEvents.readLines().findAll { it.endsWith('.properties') }

                    if (propertiesFiles) {
                        // Copy the modified/added .properties files to a target directory
                        propertiesFiles.each { propertyFile ->
                            bat "xcopy /Y /I ${workspace}\\folder1\\${propertyFile} D:\\northstar\\WEB-INF\\classes\\com\\sibisoft\\northstar\\events\\struts"
                        }
                    } else {
                        echo "No modified or added .properties files found in 'events' directory."
                    }
                }
            }
        }
    }
}
