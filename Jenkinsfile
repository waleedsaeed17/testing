pipeline {
  agent any
  
  stages {
    stage('List Commit IDs') {
      steps {
        script {
          def file = 'script.txt'
          def workspacePath = pwd()
          def commitIds = bat(script: "git -C ${workspacePath} rev-list HEAD -- ${file}", returnStdout: true).split('\n')
          
          for (def commitId : commitIds) {
            def commitDetails = bat(script: git -C ${workspacePath} show ${commitId}", returnStdout: true)
            println commitDetails
            println "---------------------------"
          }
        }
      }
    }
  }
}
