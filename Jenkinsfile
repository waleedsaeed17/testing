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
                            // Add the changed file path to the list
                            changedFiles.add(path)
                        }
                    }

                    // Print the list of changed file paths
                    echo "Changed files:"
                    changedFiles.each { file ->
                        //echo file
                    }
                }
            }
        }
    }
}
