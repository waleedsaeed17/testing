pipeline {
    agent {label 'sys'}

    stages {

        stage('Identify and Copy Files') {
            steps {
                script {
                    def workspacePath = "${env.WORKSPACE}"
                    def directories = [
                        ['sourceDir': 'tes\folder', 'targetDir': 'D:\\northstar\\WEB-INF\\classes\\com\\sibisoft\\northstar\\events\\struts'],
                        ['sourceDir': 'folder2', 'targetDir': 'D:\\northstar\\webINF']
                        // Add more directory mappings as needed
                    ]
                    
                    // Get the list of changed .properties files with added and modified filter
                    def changedFiles = bat(script: 'git diff --name-only --diff-filter=AM HEAD@{1} HEAD', returnStdout: true).trim().split("\\r?\\n")
                    echo "Changed Files: ${changedFiles}"
                    
                    for (dirMapping in directories) {
                        def sourceDir = "${workspacePath}\\${dirMapping.sourceDir}"
                        def targetDir = dirMapping.targetDir
                        echo "Source Directory: ${sourceDir}"
                        echo "Target Directory: ${targetDir}"
                        
                        def relevantFiles = []
                        for (file in changedFiles) {
                            if (file.startsWith("${dirMapping.sourceDir}/") && file.endsWith('.properties')) {
                                relevantFiles.add(file)
                            }
                        }
                        
                        echo "Relevant Files for ${dirMapping.sourceDir}: ${relevantFiles}"
                        
                        if (!relevantFiles.isEmpty()) {
                            // Create the target directory if it doesn't exist
                            bat(script: "if not exist \"${targetDir}\" mkdir \"${targetDir}\"")
                            
                            // Copy the relevant files to the target directory
                            for (file in relevantFiles) {
                                def fileName = file.substring(file.lastIndexOf('/') + 1)
                                def destinationPath = "${targetDir}\\${fileName}"
                                echo "Copying ${sourceDir}\\${fileName} to ${destinationPath}"
                                bat(script: "copy ${sourceDir}\\${fileName} ${destinationPath}")
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
