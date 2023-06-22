pipeline {
    agent {
        label 'ServerVM'
    }
    stages {
        stage('Diff Files') {
            steps {
                script {
                   // def diffCmd = "fc /W /N script.txt change.txt > final.txt"
                  //  bat "diff script.txt change.txt > final.txt"

                    bat """
                    "C:\\Program Files\\Git\\bin\\git.exe" diff --no-prefix script.txt change.txt > final.txt
                """
                   
                }
            }
        }
    }
}
