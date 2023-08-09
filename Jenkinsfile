pipeline {
    agent {label 'sys'}
    
    stages {
        
        stage('Show Changes') {
            steps {
                script {
                    def workspacePath = pwd()
                    
                    // List updated and newly added .properties files
                    def gitDiff = bat(script: 'git diff --name-only --diff-filter=AM HEAD@{1} HEAD', returnStdout: true).trim()
                    echo "Added and modified .properties files in this pull:"
                    
                    gitDiff.split('\n').findAll { filePath ->
                        filePath.endsWith('.properties')
                    }.each { propertiesFile ->
                        def fullPath = "${workspacePath}\\${propertiesFile}"
                        echo fullPath
                    }
                }
            }
        }
    }
}
