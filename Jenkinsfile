pipeline {
    agent {label 'sys'}

    stages {

        stage('Find Modified/Added .properties files') {
            steps {
                script {
                    // Use git diff command with path filters for each directory
                    def adminFiles = bat(returnStdout: true, script: 'git diff --name-only --diff-filter=MA -- "tes/*.properties"')
                    def banquetFiles = bat(returnStdout: true, script: 'git diff --name-only --diff-filter=MA -- "conf/banquet/*.properties"')
                    def campaignFiles = bat(returnStdout: true, script: 'git diff --name-only --diff-filter=MA -- "conf/campaign/*.properties"')
                    def diningFiles = bat(returnStdout: true, script: 'git diff --name-only --diff-filter=MA -- "conf/dining/*.properties"')
                    def pmsFiles = bat(returnStdout: true, script: 'git diff --name-only --diff-filter=MA -- "conf/pms/*.properties"')

                    def allModifiedFiles = adminFiles + "\n" + banquetFiles + "\n" + campaignFiles + "\n" + diningFiles + "\n" + pmsFiles
                    def propertiesFiles = allModifiedFiles.split("\\n").findAll { it.endsWith('.properties') }

                    if (propertiesFiles) {
                        // Define a map with source directories and their corresponding target locations
                        def fileMappings = [
                            "${workspace}\\conf\\admin\\": "northstar\\WEB-INF\\classes\\com\\sibisoft\\northstar\\admin\\",
                            "${workspace}\\conf\\banquet\\": "northstar\\WEB-INF\\classes\\com\\sibisoft\\northstar\\banquet\\",
                            "${workspace}\\conf\\campaign\\": "northstar\\WEB-INF\\classes\\com\\sibisoft\\northstar\\campaign\\",
                            "${workspace}\\conf\\dining\\": "northstar\\WEB-INF\\classes\\com\\sibisoft\\northstar\\dining\\",
                            "${workspace}\\conf\\pms\\": "northstar\\WEB-INF\\classes\\com\\sibisoft\\northstar\\pms\\"
                        ]

                        // Loop through the file mappings and copy the modified/added .properties files to the target locations
                        fileMappings.each { sourceDir, targetDir ->
                            bat "xcopy /Y /I /E \"${sourceDir}*.properties\" \"${workspace}\\${targetDir}\""
                        }
                    } else {
                        echo "No modified or added .properties files found."
                    }
                }
            }
        }
    }
}
