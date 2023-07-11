pipeline {
  agent any
  stages {
    stage("Show new commits") {
      steps {
        script {
          // Get the list of new commits since the last build
          def new_commits = bat (
            script: "git log --since=last-build --oneline",
            returnStdout: true
          ).trim().split("\n")

          // Print the new commits
          echo "New commits:"
          for (commit in new_commits) {
            echo "  ${commit}"
          }
        }
      }
    }
  }
}
