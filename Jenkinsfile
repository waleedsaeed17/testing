pipeline {
    agent {
        label 'ServerVM'
    }
    stages {
        stage('Compare Files') {
            steps {
                bat 'C:\\Program Files\\WinMerge\\WinMergeU.exe script.txt change.txt /r /u /wl /e /wl /wr /n'
            }
        }
        stage('Save Differences') {
            steps {
                bat 'echo off > final.txt && fc /n script.txt change.txt >> final.txt'
            }
        }
    }
}
