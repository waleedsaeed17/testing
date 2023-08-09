pipeline {
    agent { label 'sys' }

    stages {
        stage('Identify and Copy Files') {
            steps {
                script {
                    def workspacePath = "${env.WORKSPACE}"
                    def directories = [
                        ['sourceDir': 'folder1\\conf\\', 'targetDir': 'D:\\northstar\\WEB-INF\\classes\\com\\sibisoft\\northstar\\events\\struts'],
                        ['sourceDir': 'folder2//admin//', 'targetDir': 'D:\\northstar']
                        // Add more directory mappings as needed
                    ]

                    // Get the list of changed .properties files with added and modified filter
                    def changedFiles = bat(script: 'git diff --name-only --diff-filter=AM HEAD@{1} HEAD', returnStdout: true).trim().split("\\r?\\n")
                    echo "Changed Files: ${changedFiles}"

                    for (dirMapping in directories) {
                        //def sourceDir = "${workspacePath}\\${dirMapping.sourceDir}".replace("/", "\\")
                        //def targetDir = dirMapping.targetDir
                        def sourceDir = "${workspacePath}/${dirMapping.sourceDir}".replace("\\", "/").replaceAll("/+", "/")
                        def targetDir = dirMapping.targetDir.replace("\\", "/").replaceAll("/+", "/")
                        echo "Source Directory: ${sourceDir}"
                        echo "Target Directory: ${targetDir}"

                        // Filter for .properties files in the source directory and its subdirectories
                        def relevantFiles = []
                        for (file in changedFiles) {
                            echo "Checking file: ${file}"
                            echo "Source Directory: ${sourceDir}"
    
                            if (file.startsWith(sourceDir)) {
                                if (file.endsWith('.properties')) {
                                    relevantFiles.add(file)
                                } else {
                                    echo "Skipped (not .properties file): $file"
                                }
                            } else {
                                echo "Skipped (not in source directory): $file"
                            }
                        }

                        echo "All Changed Files: ${changedFiles}"
                        echo "Relevant Files for ${dirMapping.sourceDir}: ${relevantFiles}"

                        if (!relevantFiles.isEmpty()) {
                            // Create the target directory if it doesn't exist
                            bat(script: "if not exist \"${targetDir}\" mkdir \"${targetDir}\"")

                            // Copy the relevant files to the target directory
                            for (file in relevantFiles) {
                                def relativePath = file.replace(sourceDir, '')
                                def destinationPath = "${targetDir}\\${relativePath}"
                                echo "Copying ${sourceDir}${relativePath} to ${destinationPath}"
                                bat(script: "copy \"${sourceDir}${relativePath}\" \"${destinationPath}\"")
                            }
                        } else {
                            echo "No relevant files found for ${dirMapping.sourceDir}."
                        }
                    }
                }
            }
        }
    }
}
