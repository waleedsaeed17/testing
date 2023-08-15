pipeline {
    agent { label 'sys' }
    
    stages {
        stage('Copy Related Files') {
            steps {
                script {
                    def changedJavaFiles = bat(script: 'git diff --name-only --diff-filter=AM HEAD@{1} HEAD' | , returnStdout: true).trim()
                    echo "Changed Java Files:"
                    echo changedJavaFiles
                    
                    // Iterate through each changed Java file and find related files in the specified directory
                    changedJavaFiles.split('\n').each { filePath ->
                        def backslashPath = filePath.replaceAll('/', '\\\\\\\\')
                        echo "File Path: ${backslashPath}"
                        
                        // Check if the file path contains 'src\\build' and ends with '.java'
                        if (backslashPath.startsWith('src\\\\build') && backslashPath.endsWith('.java')) {
                            // Extract the base file name without extension
                            def baseFileName = backslashPath.tokenize('\\').last().replaceAll('.java', '')
                            
                            // Find related files in the destination directory
                            def relatedFiles = bat(script: "dir D:\\northstar\\WEB-INF\\classes\\${baseFileName}*", returnStdout: true).trim()
                            
                            // Copy the related files to D:\\myfiles
                            relatedFiles.split('\n').each { relatedFileLine ->
                                def relatedFileName = relatedFileLine.tokenize('\\').last().trim()
                                echo "Copying related file: ${relatedFileName}"
                                bat "xcopy /Y D:\\northstar\\WEB-INF\\classes\\${relatedFileName} D:\\myfiles\\"
                            }
                        }
                    }
                }
            }
        }
    }
}
