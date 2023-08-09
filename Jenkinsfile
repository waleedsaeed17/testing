pipeline {
    agent {label 'sys'}

    stages {

        stage('Check and Copy Files') {
            steps {
                script {
                    def workspacePath = env.WORKSPACE
                    def confPath = "${workspacePath}\\folder1\\conf"
                    def adminConfPath = "${workspacePath}\\conf\\admin"
                    def banquetConfPath = "${workspacePath}\\conf\\banquet"
                    def destinationPathEvents = "D:\\northstar\\WEB-INF\\classes\\com\\sibisoft\\northstar\\events\\struts"
                    def destinationPathAdmin = "D:\\\\northstar\\\\WEB-INF\\\\classes\\\\com\\\\sibisoft\\\\northstar\\\\admin\\\\struts"
                    def destinationPathBanquet = "D:\\\\northstar\\\\WEB-INF\\\\classes\\\\com\\\\sibisoft\\\\northstar\\\\banquet\\\\struts"

                    // List new and modified files with ".properties" extension
                    def changes = bat(script: 'git diff --name-status HEAD@{1} HEAD', returnStdout: true).trim().split('\r\n')

                    // Iterate through the changes and copy relevant ".properties" files
                    changes.each { change ->
                        def status = change.take(1)
                        def filePath = change.drop(2)

                        if (status == 'A' || status == 'M') {
                            def sourceFile = "${workspacePath}\\${filePath}"

                            if (filePath.endsWith('.properties')) {
                                if (filePath.startsWith('folder1\\conf\\')) {
                                    def destinationFile = "${destinationPathEvents}\\${filePath}"
                                    bat "xcopy /Y \"${sourceFile}\" \"${destinationFile}\""
                                } else if (filePath.startsWith('conf/admin/')) {
                                    def destinationFile = "${destinationPathAdmin}\\${filePath}"
                                    bat "xcopy /Y \"${sourceFile}\" \"${destinationFile}\""
                                } else if (filePath.startsWith('conf/banquet/')) {
                                    def destinationFile = "${destinationPathBanquet}\\${filePath}"
                                    bat "xcopy /Y \"${sourceFile}\" \"${destinationFile}\""
                                }
                            }
                        }
                    }
                }
            }
        }
    }
}
