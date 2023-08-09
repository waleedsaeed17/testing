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
                            if (file.startsWith('folder1/conf')) {
                                copyFile(file, "D:\\northtar\\${getFilenameFromPath(file)}")
                            } else if (file.startsWith('folder2/admin')) {
                                copyFile(file, "D:\\northstar\\classes\\${getFilenameFromPath(file)}")
                            }
                        }
                    }
                }
            }
        }
    }
}

def copyFile(sourcePath, destinationPath) {
    def sourceFile = new File(sourcePath)
    def destinationFile = new File(destinationPath)
    
    destinationFile.parentFile.mkdirs()
    sourceFile.eachByte { destinationFile.append(it) }
    
    echo "Copied ${sourcePath} to ${destinationPath}"
}

def getFilenameFromPath(filePath) {
    return filePath.substring(filePath.lastIndexOf('/') + 1)
}
