pipeline {
    agent any
    
    stages {
        
        stage('Check for changes') {
            steps {
                script {
                    // Get the list of changed files since the last build
                    def changeLogSets = currentBuild.changeSets
                    def changedFiles = []
                    
                    for (int i = 0; i < changeLogSets.size(); i++) {
                        def entries = changeLogSets[i].items
                        for (int j = 0; j < entries.length; j++) {
                            def entry = entries[j]
                            def affectedFiles = entry.affectedFiles
                            for (int k = 0; k < affectedFiles.size(); k++) {
                                def file = affectedFiles[k]
                                // Check if the file path matches the specific file you want
                                if (file.path == 'C:\ProgramData\Jenkins\.jenkins\workspace\testing\\script.txt') {
                                    changedFiles.add(file)
                                }
                            }
                        }
                    }
                    
                    // Print the changes or "No changes" if there are none
                    if (changedFiles.isEmpty()) {
                        echo 'No changes'
                    } else {
                        for (def file : changedFiles) {
                            // Retrieve the content of the changed file
                            def fileContent = readFile(file.path)
                            echo "Changes in ${file.path}: ${fileContent}"
                        }
                    }
                }
            }
        }
    }
}
