pipeline {
    agent {label 'sys'}
    
    stages {
        
        stage('Check and Copy') {
            steps {
                script {
                    def workspace = pwd()
                    def changes = sh(script: "git diff --name-status HEAD^..HEAD", returnStdout: true).trim().split('\n')
                    
                    def copyRules = [
                        ["source": "${workspace}\\folder1\\conf", "target": "D:\\northstar\\sibisoft1"],
                        ["source": "folder2", "target": "D:\\northstar\\sibisoft2"],
                        // Add more rules as needed
                    ]
                    
                    for (change in changes) {
                        def fileInfo = change.split('\t')
                        def changeType = fileInfo[0]
                        def filePath = fileInfo[1]
                        
                        for (rule in copyRules) {
                            def sourceDir = rule.source
                            def targetDir = rule.target
                            
                            if (filePath.startsWith(sourceDir) && (changeType == "M" || changeType == "A")) {
                                def fileName = filePath.substring(filePath.lastIndexOf('/') + 1)
                                def destFilePath = "${targetDir}/${fileName}"
                                
                                bat "xcopy /Y \"${workspace}/${filePath}\" \"${destFilePath}\""
                                echo "Copied ${fileName} to ${destFilePath}."
                            }
                        }
                    }
                }
            }
        }
    }
}
