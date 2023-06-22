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
          def latestCommit = bat(script: 'git rev-parse HEAD', returnStdout: true).trim()

          // Retrieve the new commit hashes
          def commitHashes = bat(script: "git log --pretty=format:%h ${latestCommit}..HEAD", returnStdout: true).trim().split('\r\n')

          // Initialize the commit content variable
          def commitContent = ""

          // Iterate over the commit hashes
          for (def commitHash in commitHashes) {
            // Retrieve the commit content for the specific file
            def fileContent = bat(script: "git show ${commitHash}:D:\\Tools\\jenkins-agent\\workspace\\test\\testing\\script.txt", returnStdout: true).trim()

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
