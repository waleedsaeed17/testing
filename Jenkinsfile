pipeline {
    agent {label 'sys'}

    stages {

        stage('Run Git Commands') {
            steps {
                // Change to the workspace directory
                dir("${WORKSPACE}") {
                    // Run the Git commands and print the absolute paths of modified and newly added files
                    powershell """
                    Write-Output "=== Modified and New Added Files ==="
                    git diff --name-only --diff-filter=AM HEAD^ HEAD | ForEach-Object { (Get-Item -LiteralPath \$_).FullName }
                    """
                }
            }
        }
    }
}
