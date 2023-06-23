pipeline {
    agent {
        label 'ServerVM'
    }
    
    stages {
        stage('Compare Files') {
            steps {
                bat 'FC /W "script.txt" "change.txt" > final.txt'
            }
        }
    }
}
