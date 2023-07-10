pipeline {
  agent {
    label "sys"
  }
  stages {
    stage("Extract new commited code") {
      steps {
        script {
          def lastBuild = sh(returnStdout: true, script: "git log -1 --format=%H")
          def newCommits = sh(returnStdout: true, script: "git log ${lastBuild}..HEAD --oneline")
          def gitFile = "D:\jenkins_agent\workspace\testing\script.txt"
          def newCommitsList = newCommits.split("\n")
          for (def commit in newCommitsList) {
            def commitHash = commit.substring(0, 7)
            sh(script: "git checkout ${commitHash} ${gitFile}")
          }
        }
      }
    }
  }
}
