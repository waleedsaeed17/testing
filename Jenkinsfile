pipeline {
    agent { label 'sys' }
    
    stages {
        stage('Copy Related Files') {
            steps {
                script {
                    def changedFiles = bat(script: 'git diff --name-only --diff-filter=AM HEAD@{1} HEAD', returnStdout: true).trim()

                    echo "Changed Files:"
                    echo changedFiles

                    // Iterate through each changed file and find related files in the specified directory
                    changedFiles.split('\n').each { filePath ->
                        def backslashPath = filePath.replaceAll('/', '\\\\\\\\')
                        echo "File Path: ${backslashPath}"
                        
                        if (backslashPath.startsWith('src\\\\build') && backslashPath.endsWith('.java')) {
                            def baseFileName = backslashPath.tokenize('\\').last().replaceAll('.java', '')
                            
                            def relatedFiles = bat(script: "dir D:\\northstar\\WEB-INF\\classes\\${baseFileName}*", returnStdout: true).trim()

                            echo "Related Files:"
                            echo relatedFiles
                            
                            relatedFiles.split('\n').each { relatedFileLine ->
                                def relatedFileName = relatedFileLine.tokenize('\\').last().trim()
                                echo "Copying related file: ${relatedFileName}"
                                //bat "xcopy /Y D:\\northstar\\WEB-INF\\classes\\${relatedFileName} D:\\myfiles\\" > NUL
                                //bat 'xcopy /Y "D:\\northstar\\WEB-INF\\classes\\"${relatedFileName} "D:\\myfiles\\" > NUL'
                                //bat "xcopy /Y \"D:\\northstar\\WEB-INF\\classes\\${relatedFileName}\" \"D:\\myfiles\\\"  1>NUL"
                                bat """xcopy /Y "D:\\northstar\\WEB-INF\\classes\\${relatedFileName}" "D:\\myfiles\\"  1>NUL"""


                            }
                        }
                    }
                }
            }
        }
    }
}
