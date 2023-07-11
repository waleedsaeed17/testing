pipeline {
  agent any
  stages {
    stage('List Commit IDs') {
      steps {
        script {
          def file = 'script.txt'
          def commitIds = bat (script: "git rev-list HEAD -- $file", returnStdout: true).split('\n')
          println "Commit IDs are: $commitIds"

          for (commitId in commitIds) {
            println "Code for commit ID $commitId:"
            bat (script: "git show $commitId")
          }
        }
      }
    }
  }
}
