pipeline {
    agent { label ' ServerVM ' }

    stages {
        stage('Git Diff') {
            steps {
                bat """
                    del changes.txt
                    "C:\\Program Files\\Git\\bin\\git.exe" diff --no-prefix HEAD~1 HEAD D:\\Tools\\jenkins-agent\\workspace\\test\\script.txt > changes.txt
                """
            }
        }
    }
}
