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
                    def winmergePath = "C:\\Program Files\\WinMerge\\WinMergeU.exe"
                    def deltaPath = "final.txt"
                    start "${winmergePath} ${file1} ${file2} /o ${deltaPath}"
                }
            }
        }
    }
}
