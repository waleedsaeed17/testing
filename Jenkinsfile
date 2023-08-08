pipeline {
    agent {label 'sys'}

    stages {
        
        stage('Find .properties files') {
            steps {
                script {
                    def modifiedFilesEvents = bat(returnStdout: true, script: 'git diff --name-only --diff-filter=AM HEAD@{1} HEAD')
                    def propertiesFiles = modifiedFilesEvents.split("\\n").findAll { it.endsWith('.properties') }

                    if (propertiesFiles) {
                        // Copy the modified/added .properties files to a target directory
                        bat "xcopy /Y /I /E ${workspace}\\folder1\\*.properties D:\\northstar\\WEB-INF\\classes\\com\\sibisoft\\northstar\\events\\struts"
                    } else {
                        echo "No modified or added .properties files found in 'events' directory."
                    }
                }

                script {
                    def modifiedFilesAdmin = bat(returnStdout: true, script: 'git diff --name-only --diff-filter=AM HEAD@{1} HEAD')
                    def propertiesFilesAdmin = modifiedFilesAdmin.split("\\n").findAll { it.endsWith('.properties') }

                    if (propertiesFilesAdmin) {
                        // Copy the modified/added .properties files to a target directory
                        bat "xcopy /Y /I /E ${workspace}\\folder2\\*.properties D:\\northstar\\WEB-INF\\classes\\com\\sibisoft\\northstar\\admin"
                    } else {
                        echo "No modified or added .properties files found in 'admin' directory."
                    }
                }
            }
        }

    }
}
