pipeline {
    agent { label ' ServerVM ' }

    stages {
        stage('Git Diff') {
            steps {
                bat 'del D:\\Tools\\jenkins-agent\\workspace\\test\\extracted.txt'
                 
                    // "C:\\Program Files\\Git\\bin\\git.exe" show -p --no-prefix HEAD D:\\Tools\\jenkins-agent\\workspace\\test\\script.txt > changes.txt
                bat "C:\\Program Files\\Git\\bin\\git.exe" diff --no-prefix HEAD~1 HEAD D:\\Tools\\jenkins-agent\\workspace\\test\\script.txt > extracted.txt
                """
            }
        }
    }
}
