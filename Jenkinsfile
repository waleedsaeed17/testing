pipeline {
    agent {label 'sys'}
    
    environment {
        PATCH_UTILITY_JAR = 'D:\\PatchUtility\\PatchUtility.jar'
        PATCH_FILE = 'D:\\PatchUtility\\patch1.zip'
        WORKSPACE_DIR = 'D:\\jenkins\\workspace\\M65'
        TOMCAT_DIR = 'D:\\Northstar\\Tomcat-9.0.75'
        HASH1 = '642f56e564f04c13e50dcc3ed8cf58b51e70f449'
        HASH2 = '0d7cfbe841757a56d880e21a41de94780a677b52'
    }
    
    stages {
    
        stage('Checking Deleted files') {
            steps {
                dir(WORKSPACE_DIR) {
                    // Run the Git command and print the complete path of deleted files
                    script {
                        //def gitDeleted = bat(returnStdout: true, script: "git diff --name-only --diff-filter=AM " + HASH1 + " " + HASH2)
                        def gitDeleted = bat(returnStdout: true, script: "git diff --name-only --diff-filter=AM HEAD@{1} HEAD")
                        def workspacePath = pwd() // Get the current workspace path
                        gitDeleted.readLines().each { fileName ->
                            echo "Deleted Files: ${workspacePath}\\${fileName}"
                        }
                    }
                }
            }
        }
        stage('Patch Created') {
            steps {
                echo 'Patch Created'
            }
        }
    }
}
