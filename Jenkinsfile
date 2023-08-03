pipeline {
  agent any
  options {
        ansiColor('xterm')
  }
  stages {
    stage('MobSF-Scan') {
      steps {
        sh 'mobsfscan iOS/MSTG-JWT/ --json -o mobscan.json'
      }
    }
    stage('Push to DefectDojo') {
            environment {
                DEFECTDOJO_API_KEY = credentials('DefectDojo-API-Token')  // Your DefectDojo API key credentials ID
                DEFECTDOJO_URL = 'https://defectdojo.dalmiabharat.com/'  // Replace with your DefectDojo URL
            }
            steps {
                script {
                    def scanJSONPath = "${WORKSPACE}/mobscan.json"
                    def scanJSONContent = readFile file: scanJSONPath
                    def defectDojoPayload = [
                        engagement: 'Mobsfscan Report',
                        test_type: 'Mobsfscan Scan',
                        file: scanJSONContent
                    ]

                    // Upload scan JSON to DefectDojo
                    def response = httpRequest(
                        acceptType: 'APPLICATION_JSON',
                        contentType: 'APPLICATION_JSON',
                        customHeaders: [[name: 'Authorization', value: "Token ${DEFECTDOJO_API_KEY}"]],
                        httpMode: 'POST',
                        requestBody: groovy.json.JsonOutput.toJson(defectDojoPayload),
                        responseHandle: 'NONE',
                        url: "${DEFECTDOJO_URL}/api/v2/import-scan/"
                    )

                    if (response.status == 201) {
                        echo "Scan JSON uploaded successfully to DefectDojo."
                    } else {
                        echo "Failed to upload the scan JSON to DefectDojo. Status: ${response.status}"
                    }
                }
            }
        }
  }
}
