pipeline {
    agent {label 'sys'}

    stages {

        stage('Identify and Copy Files') {
            steps {
                script {
                    def workspacePath = "${env.WORKSPACE}"
                    def directories = [
                        ['sourceDir': 'folder1', 'targetDir': 'D:\\northstar\\classes'],
                        ['sourceDir': 'folder2', 'targetDir': 'D:\\northstar\\webINF']
                        // Add more directory mappings as needed
                    ]
                    
                    // Get the list of changed .properties files
                    def changedFiles = bat(script: 'git diff --name-only --diff-filter=AM HEAD@{1} HEAD', returnStdout: true).trim().split("\\r?\\n")
                    
                    for (dirMapping in directories) {
                        def sourceDir = "${workspacePath}\\${dirMapping.sourceDir}"
                        def targetDir = dirMapping.targetDir
                        
                        def relevantFiles = []
                        for (file in changedFiles) {
                            if (file.startsWith("${dirMapping.sourceDir}/") && file.endsWith('.properties')) {
                                relevantFiles.add(file)
                            }
                        }
                        
                        echo "Relevant Files for ${dirMapping.sourceDir}: ${relevantFiles}"
                        
                        // Copy the relevant files to the target directory
                        for (file in relevantFiles) {
                            def fileName = file.substring(file.lastIndexOf('/') + 1)
                            def destinationPath = "${targetDir}\\${fileName}"
                            bat(script: "copy ${sourceDir}\\${fileName} ${destinationPath}")
                        }
                    }
                }
            }
        }
    }
}
