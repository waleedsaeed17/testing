pipeline {
    agent {label 'sys'}

    stages {

        stage('Fetch Modified and Added .properties Files') {
            steps {
                script {
                    def modifiedAndAddedFiles = bat(script: 'git diff --name-only --diff-filter=AM HEAD@{1} HEAD', returnStdout: true).trim()
                    def filesArray = modifiedAndAddedFiles.split('\r\n')

                    echo "Modified and Added .properties Files:"
                    for (String file : filesArray) {
                        if (file.endsWith('.properties')) {
                            echo file

                            // Check the containing directories and copy files accordingly
                            if (file.startsWith('folder1\conf')) {
                                bat "xcopy /Y \"${file}\" \"D:\\northtar\\\\${file.substring('folder1/conf/'.length())}\""
                            } else if (file.startsWith('folder2/admin')) {
                                bat "xcopy /Y \"${file}\" \"D:\\northstar\\\\classes\\\\${file.substring('folder2/admin/'.length())}\""
                            }
                        }
                    }
                }
            }
        }
    }
}
