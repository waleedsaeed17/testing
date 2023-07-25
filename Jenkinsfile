pipeline {
    agent {label 'sys'}

    stages {

        stage('Run Git Commands') {
            steps {
                // Change to the workspace directory
                dir("${WORKSPACE}") {
                    // Run the Git commands with echo for the heading
                    echo "=== Modified and New Added Files ==="
                    bat """
                    for /f \"tokens=*\" %%i in ('git diff --name-only --diff-filter=AM HEAD@{1} HEAD') do (
                        for /f \"tokens=*\" %%a in ('git rev-parse --show-toplevel/%%i') do (
                            echo %%a
                        )
                    )
                    """
                }
            }
        }
    }
}
