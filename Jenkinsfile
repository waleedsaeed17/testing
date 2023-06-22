pipeline {
    agent {
        label 'ServerVM'
    }
    stages {
        stage('Diff Files') {
            steps {
                script {
                    def diffCmd = "fc /W /N script.txt change.txt > final.txt"
                    bat diffCmd
                }
            }
        }
    }
}
