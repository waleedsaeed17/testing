pipeline {
    agent { label ' Node138-2 ' }

    stages {
        stage('Git Diff') {
            steps {
                bat """
                    "C:\\Program Files\\Git\\bin\\git.exe" diff --no-prefix HEAD~1 HEAD D:\\Tools\\jenkins-agent\\workspace\\test\\script.txt > changes.txt
                """
            }
        }
    }
}
