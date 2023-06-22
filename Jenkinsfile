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
        stage('Print Diff') {
            steps {
                script {
                    def changeFile = readFile 'final.txt'
                    echo "Diff Output:\n${changeFile}"
                }
            }
        }
    }
}
