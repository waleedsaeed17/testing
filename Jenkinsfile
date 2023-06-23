pipeline {
    agent {
        label "ServerVM"
    }
    stages {
        stage("Compare files") {
            steps {
                withCredentials([file(credentialsId: 'winmerge-api-key', variable: 'API_KEY')]) {
                    httpRequest(
                        url: "https://api.winmerge.com/compare",
                        method: "POST",
                        requestBody: """
                            {
                                "file1": "script.txt",
                                "file2": "change.txt",
                                "excludeSimilar": true,
                                "apiKey": "${API_KEY}"
                            }
                        """,
                        contentType: "application/json"
                    )

                    writeFile(
                        file: "output.txt",
                        content: "${httpResponse.content}"
                    )
                }
            }
        }
    }
}
