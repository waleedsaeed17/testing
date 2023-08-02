pipeline {
    agent {label 'sys'}

    stages {
        stage('Find Modified/Added .properties files') {
            steps {
                script {
                    def modifiedFiles = bat(returnStdout: true, script: 'git diff --name-only --diff-filter=AM HEAD@{1} HEAD')
                    def propertiesFiles = modifiedFiles.split("\\n").findAll { it.endsWith('.properties') }

                    if (propertiesFiles) {
                        // Copy the modified/added .properties files to a target directory
                        bat "xcopy /Y /I /E ${workspace}\\conf\\events\\*.properties ${workspace}\\target_directory\\"
                    } else {
                        echo "No modified or added .properties files found."
                    }
                }
            }
        }
    }
}
