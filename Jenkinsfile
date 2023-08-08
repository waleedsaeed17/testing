pipeline {
    agent { label 'sys' }

    stages {
        stage('Find files') {
            steps {
                script {
                    def modifiedFilesEvents = bat(returnStdout: true, script: 'git diff --name-only --diff-filter=AM HEAD@{1} HEAD')
                    def propertiesFiles = modifiedFilesEvents.readLines().findAll { it.endsWith('.properties') }

                    if (propertiesFiles) {
                        for (def file in propertiesFiles) {
                            // Copy each modified/added .properties file to the target directory
                            bat "xcopy /Y /I ${file} D:\\northstar\\WEB-INF\\classes\\com\\sibisoft\\northstar\\events\\struts"
                        }
                    } else {
                        echo "No modified or added .properties files found in 'events' directory."
                    }
                }
            }
        }
    }
}
