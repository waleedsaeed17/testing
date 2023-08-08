pipeline {
    agent { label 'sys' }

    stages {
        stage('Find and Copy Committed .properties files') {
            steps {
                script {
                    def committedFilesEvents = bat(returnStdout: true, script: 'git diff --name-only --diff-filter=AM HEAD@{1} HEAD')
                    def committedPropertiesFiles = committedFilesEvents.readLines().findAll { it.endsWith('.properties') && it.startsWith("${workspace}\\conf\\events\\") }

                    if (committedPropertiesFiles) {
                        for (def file in committedPropertiesFiles) {
                            // Copy each committed .properties file to the target directory
                            bat "xcopy /Y /I ${file} D:\\northstar\\WEB-INF\\classes\\com\\sibisoft\\northstar\\events\\struts"
                        }
                    } else {
                        echo "No committed .properties files found in 'events' directory."
                    }
                }
            }
        }
    }
}
