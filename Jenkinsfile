pipeline {
  agent any
  stages {
    stage('List Commit IDs') {
      steps {
        script {
          def file = 'script.txt'
          def commitIds = sh(script: "git rev-list HEAD -- $file", returnStdout: true).split('\n')
          println "Commit IDs are: $commitIds"
        }
      }
    }
  }
}
