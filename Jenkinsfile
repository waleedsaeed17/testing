pipeline {
  agent { label 'ServerVM ' } 

  stages {
    stage('Checkout') {
      steps {
        // Checkout the repository
        git branch: 'master', url: 'https://github.com/waleedsaeed17/testing.git'
      }
    }

    stage('Get Commit Changes') {
      steps {
        script {
          // Retrieve the latest commit hash
          def latestCommit = sh(returnStdout: true, script: 'git rev-parse HEAD').trim()

          // Retrieve the new commit hashes
          def commitHashes = sh(returnStdout: true, script: "git log --pretty=format:%h ${latestCommit}..HEAD").trim().split('\n')

          // Initialize the commit content variable
          def commitContent = ""

          // Iterate over the commit hashes
          for (def commitHash in commitHashes) {
            // Retrieve the commit content for the specific file
            def fileContent = sh(returnStdout: true, script: "git show ${commitHash}:D:\\Tools\\jenkins-agent\\workspace\\test\\testing\\script.txt").trim()

            // Append the commit content to the overall changes
            commitContent += "Commit: ${commitHash}\n\n${fileContent}\n\n"
          }

          // Save the commit content to a file
          writeFile file: '..\\change.txt', text: commitContent
        }
      }
    }
  }
}
