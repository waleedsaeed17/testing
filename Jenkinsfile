pipeline {
  agent any
  stages {
    stage("Extract new commits") {
      steps {
        script {
          // Get the list of new commits since the last build
          def new_commits = sh(
            script: "git log --since=last-build --oneline",
            returnStdout: true
          ).trim().split("\n")

          // Write the new commits to a file
          writeFile(
            file: "script.txt",
            text: new_commits
          )
        }
      }
    }
  }
}
