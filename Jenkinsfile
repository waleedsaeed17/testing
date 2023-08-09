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
                            if (file.startsWith('folder1\\conf')) {
                                bat "xcopy /Y \"${file}\" \"D:\\northtar\""
                        
                        }
                    }
                }
            }
        }
    }
}
