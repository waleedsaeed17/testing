pipeline {
    agent {label 'sys'}

    stages {
        
        stage('Find Modified/Added .properties files') {
            steps {
                script {
                    // Execute a shell/batch script and capture the output (modifiedFiles)
                    def modifiedFiles = bat(returnStdout: true, script: 'git diff --name-only --diff-filter=MA origin/master...HEAD')

                    // Split the output by newlines and filter the .properties files
                    def propertiesFiles = modifiedFiles.split("\\n").findAll { it.endsWith('.properties') }

                    if (propertiesFiles) {
                        // Define a map with source directories and their corresponding target locations
                        def fileMappings = [
                            "${workspace}\\conf\\admin\\*.properties": "northstar/WEB-INF/classes/com/sibisoft/northstar/admin/",
                            "${workspace}\\conf\\banquet\\*.properties": "northstar/WEB-INF/classes/com/sibisoft/northstar/banquet/",
                            "${workspace}\\conf\\campaign\\*.properties": "northstar/WEB-INF/classes/com/sibisoft/northstar/campaign/",
                            "${workspace}\\conf\\dining\\*.properties": "northstar/WEB-INF/classes/com/sibisoft/northstar/dining/",
                            "${workspace}\\conf\\pms\\*.properties": "northstar/WEB-INF/classes/com/sibisoft/northstar/pms/"
                        ]

                        // Loop through the file mappings and copy the modified/added .properties files to the target locations
                        fileMappings.each { sourceDir, targetDir ->
                            bat "xcopy /Y /I /E ${sourceDir} ${workspace}\\${targetDir}"
                        }
                    } else {
                        echo "No modified or added .properties files found."
                    }
                }
            }
        }
    }
}
