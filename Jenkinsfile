pipeline {
  agent any
  
  stages {
    stage('List Commit IDs') {
      steps {
        script {
          def file = 'script.txt'
          def commitIds = bat(script: "git rev-list HEAD -- $file", returnStdout: true).split('\n')
          
          for (def commitId : commitIds) {
            def commitDetails = bat(script: "git show --format='%h%n%an%n%ae%n%ad%n%s' $commitId", returnStdout: true)
            println "Commit ID: $commitId"
            println "Commit Details:\n$commitDetails"
            println "---------------------------"
          }
        }
      }
    }
  }
}
