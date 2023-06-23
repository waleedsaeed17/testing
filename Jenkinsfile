pipeline {
    agent {
        label "ServerVM"
    }
    stages {
        stage("Compare files") {
            steps {
                script {
                    def file1 = "script.txt"
                    def file2 = "change.txt"
                    def winmergePath = "C:\\Program Files\\WinMerge\\winmerge.exe"
                    def deltaPath = "final.txt"
                    sh "${winmergePath} ${file1} ${file2} /o ${deltaPath}"
                }
            }
        }
    }
}
