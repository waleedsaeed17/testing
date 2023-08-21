pipeline {
    agent {label 'sys'}

    stages {

        stage('Search and Copy Files') {
            steps {
                // Run the git diff command to list modified files and print them
                script {
                    def modifiedFiles = bat(script: 'git diff --name-only --diff-filter=AM HEAD@{1} HEAD', returnStdout: true).trim()
                    def fileList = modifiedFiles.readLines()

                    fileList.each { file ->
                        if (file.startsWith('src\\build') && file.endsWith('xyz.java')) {
                            echo "Modified Java file found: ${file}"

                            // Extract the filename without extension (xyz)
                            def baseFileName = file.tokenize('\\').last().replaceAll('.java', '')

                            // Search for files containing the base file name in D:\northstar\WEB-INF\classes
                            def searchResults = bat(script: "dir /s /b D:\\northstar\\WEB-INF\\classes\\*${baseFileName}*", returnStdout: true).trim()
                            def searchResultList = searchResults.readLines()

                            if (!searchResultList.empty) {
                                echo "Matching files found:"
                                searchResultList.each { matchingFile ->
                                    // Replace forward slashes with backslashes in the path
                                    def matchingFilePath = matchingFile.replace('/', '\\')
                                    echo " - ${matchingFilePath}"
                                    // Copy matching files to D:\myfiles directory using xcopy
                                    bat "xcopy /Y \"${matchingFilePath}\" \"D:\\myfiles\""
                                }
                            } else {
                                echo "No matching files found."
                            }
                        }
                    }
                }
            }
        }
    }
}
