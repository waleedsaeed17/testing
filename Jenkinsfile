pipeline {
  agent { label 'sys' }
    
  stages {
    stage('Retrieve New Commits') {
      steps {
        script {
          // Specify the file path
          def filePath = 'D:\\jenkins_agent\\workspace\\test\\script.txt'

          // Get the timestamp of the last successful build
          def lastBuildTimestamp = null
          def lastSuccessfulBuild = currentBuild.previousSuccessfulBuild
          if (lastSuccessfulBuild != null) {
            lastBuildTimestamp = lastSuccessfulBuild.timestamp.toISOString()
          }

          // Use the 'git log' command with the '--since' option to retrieve the new commits
          def gitLogCmd = "git log --follow --pretty=oneline --since=\"${lastBuildTimestamp}\" -- ${filePath}"
          def commitLogs = bat(script: "cmd /C \"${gitLogCmd}\"", returnStdout: true).trim().split('\n')

          // Iterate over the new commit hashes and retrieve the actual code changes using 'git show'
          for (commitLog in commitLogs) {
            def commitHash = commitLog.split()[0]
            def gitShowCmd = "git show ${commitHash}:${filePath}"
            def codeChanges = bat(script: "cmd /C \"${gitShowCmd}\"", returnStdout: true).trim()

            // Do whatever you need with the code changes
            echo "Code changes for commit ${commitHash}:\n${codeChanges}"
          }
        }
      }
    }
  }
}
