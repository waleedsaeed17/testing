pipeline {
    agent {label 'sys'}
    
    stages {
        
        stage('Copy Modified Properties Files') {
            steps {
                script {
                    // Define a list of source and target directories
                    def directoryMappings = [
                        [source: 'folder1\\conf', target: 'D:\\northstar'],
                        [source: 'source_dir_2', target: 'target_dir_2']
                        // Add more mappings as needed
                    ]
                    
                    // Get the list of modified/added .properties files using git diff
                    def modifiedPropertiesFiles = bat(script: 'git diff --name-only --diff-filter=AM HEAD@{1} HEAD | findstr /R "\\.properties$"', returnStdout: true).trim().split('\r\n')
                    
                    // Loop through each directory mapping
                    directoryMappings.each { mapping ->
                        // Use PowerShell to copy modified/added .properties files
                        powershell '''
                            $sourceDir = "${env.WORKSPACE}\\${mapping.source}"
                            $targetDir = "${env.WORKSPACE}\\${mapping.target}"
                            
                            # Create the target directory if it doesn't exist
                            if (-not (Test-Path -Path $targetDir)) {
                                New-Item -Path $targetDir -ItemType Directory
                            }
                            
                            # Loop through each modified/added .properties file
                            foreach ($file in $modifiedPropertiesFiles) {
                                $filePath = Join-Path $sourceDir $file
                                if (Test-Path -Path $filePath) {
                                    Copy-Item -Path $filePath -Destination $targetDir
                                }
                            }
                        '''
                    }
                }
            }
        }
    }
}
