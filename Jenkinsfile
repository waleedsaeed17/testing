pipeline {
  agent any
  stages {
    stage("Show new commits") {
      steps {
        script {
          // Get the list of new commits since the last build for the file "script.txt"
          def new_commits = sh(
            script: "git log --since=last-build --oneline -- path=script.txt",
            returnStdout: true
          ).trim().split("\n")

          // Print the new commits
          echo "New commits for script.txt:"
          for (commit in new_commits) {
            echo "  ${commit}"
          }
        }
      }
    }
  }
}
