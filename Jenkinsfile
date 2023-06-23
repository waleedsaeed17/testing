pipeline {
    agent {
        label "ServerVM"
    }
    stages {
        stage("Start a process") {
            steps {
                durableTask(
                    id: "my-task",
                    command: "cmd /c start C:\\Program Files\\WinMerge\\WinMergeU.exe script.txt change.txt /o final.txt"
                )
            }
        }
    }
}
