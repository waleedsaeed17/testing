pipeline {
  agent any
  
  stages {
    stage('List Commit IDs') {
      steps {
        script {
          def file = 'script.txt'
          def commitIds = bat(script: "git rev-list HEAD -- $file", returnStdout: true).split('\n')
          
          for (def commitId : commitIds) {
            def commitDetails = bat(script: "git show --format=\"Commit ID: %h%nAuthor: %an <%ae>%nDate: %ad%nMessage: %s\" $commitId", returnStdout: true)
            println commitDetails
            println "---------------------------"
          }
        }
      }
    }
  }
}
