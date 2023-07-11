pipeline {
  agent any
  
  stages {
    stage('List Commit IDs') {
      steps {
        script {
          def file = 'script.txt'
          def commitIds = bat (script: "git rev-list HEAD -- $file", returnStdout: true).split('\n')
          
          for (def commitId : commitIds) {
            def commitDetails = bat (script: "git show $commitId", returnStdout: true)
            println commitDetails
            println "---------------------------"
          }
        }
      }
    }
  }
}
