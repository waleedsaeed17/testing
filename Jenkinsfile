pipeline {
    agent {label 'sys'}

    stages {

        stage('Get Changed Files') {
            steps {
                script {
                    def changeLog = currentBuild.changeSets[0]
                    def changedFiles = []
                    
                    // Loop through all the individual changes in the current build
                    changeLog.items.each { change ->
                        // Loop through all affected paths in the change
                        change.affectedPaths.each { path ->
                            // Replace forward slashes with four backslashes for a literal backslash
                            def filePath = path.replaceAll("/", "\\\\\\\\")
                            // Add the changed file path to the list
                            changedFiles.add(filePath)
                        }
                    }

                    // Print the list of changed file paths
                    echo "Changed files:"
                    changedFiles.each { file ->
                        echo file
                    }

                    // Iterate through changed files and copy matching files to D:\northstar
                    for (def file in changedFiles) {
                        // Check if the file path matches the specified pattern
                        if (file =~ /.*folder1\\\\conf.*/) {
                            // Extract the filename from the path
                            def fileName = file.tokenize("\\")[-1]
                            // Copy the file to D:\northstar directory
                            bat "xcopy /Y \"$file\" \"D:\\\\northstar\\\\\""
                        }
                    }
                }
            }
        }
    }
}
