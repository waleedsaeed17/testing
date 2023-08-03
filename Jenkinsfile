pipeline {
    agent {label 'sys'}

    stages {


        stage('Find Modified/Added .properties files') {
            steps {
                script {
                    def modifiedFiles = bat(returnStdout: true, script: 'git diff --name-only --diff-filter=AM HEAD@{1} HEAD')
                    def propertiesFiles = modifiedFiles.split("\\n").findAll { it.endsWith('.properties') }

                    if (propertiesFiles) {
                        // Copy the modified/added .properties files to their respective target directories
                        propertiesFiles.each { file ->
                            if (file.startsWith('tes//folder//')) {
                                bat "xcopy /Y /I /E ${workspace}\\${file} ${workspace}\\northstar\\WEB-INF\\classes\\com\\sibisoft\\northstar\\events\\struts\\"
                            } else if (file =~ '^conf/admin/') {
                                bat "xcopy /Y /I /E ${workspace}\\${file} ${workspace}\\northstar\\WEB-INF\\classes\\com\\sibisoft\\northstar\\admin\\"
                            } else if (file =~ '^conf/banquet/') {
                                bat "xcopy /Y /I /E ${workspace}\\${file} ${workspace}\\northstar\\WEB-INF\\classes\\com\\sibisoft\\northstar\\banquet\\"
                            }
                            // Add other conditions for the remaining paths and target directories
                            // ...
                            else {
                                echo "No target directory found for ${file}."
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
