import hudson.model.*

pipeline {
  agent any

  stages {
    stage('Retrieve New Commits') {
      steps {
        script {
          // Specify the file path
          def filePath = 'D:\\jenkins_agent\\workspace\\test\\scipt.txt'

          // Get the timestamp of the last successful build
          def lastBuildTimestamp = null
          def lastSuccessfulBuild = getPreviousSuccessfulBuild()
          if (lastSuccessfulBuild != null) {
            lastBuildTimestamp = lastSuccessfulBuild.getTimeInMillis().toString()
          }

          // Use the 'git log' command with the '--since' option to retrieve the new commits
          def gitLogCmd = "git log --follow --pretty=oneline --since=\"${lastBuildTimestamp}\" -- ${filePath}"
          def commitLogs = sh(script: gitLogCmd, returnStdout: true).trim().split('\n')

          // Iterate over the new commit hashes and retrieve the actual code changes using 'git show'
          for (commitLog in commitLogs) {
            def commitHash = commitLog.split()[0]
            def gitShowCmd = "git show ${commitHash}:${filePath}"
            def codeChanges = sh(script: gitShowCmd, returnStdout: true).trim()

            // Do whatever you need with the code changes
            echo "Code changes for commit ${commitHash}:\n${codeChanges}"
          }
        }
      }
    }
  }
}

// Helper function to retrieve the previous successful build
def getPreviousSuccessfulBuild() {
  def currentBuild = Thread.currentThread().executable
  def previousBuild = currentBuild.previousBuild

  while (previousBuild != null && previousBuild.result != Result.SUCCESS) {
    previousBuild = previousBuild.previousBuild
  }

  return previousBuild
}
