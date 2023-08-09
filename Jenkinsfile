pipeline {
  agent any
  options {
        ansiColor('xterm')
  }
  stages {
    stage('MobSF-Scan') {
      steps {
        sh 'mobsfscan iOS/MSTG-JWT/ --json -o mobsfscan.json'
      }
    }
    stage('Generate Engagement Name') {
            steps {
                script {
                    def engagementName = "Engagement-${BUILD_NUMBER}-${currentBuild.timestamp.format('yyyyMMdd-HHmmss')}"
                    echo "Generated Engagement Name: ${engagementName}"

                    // Store the engagementName in an environment variable
                    env.ENGAGEMENT_NAME = engagementName
                }
            }
        }
    stage('Push to DefectDojo') {
      steps {
        script {
        // def engagementName = "Engagement-${BUILD_NUMBER}-${currentBuild.timestamp.format('yyyyMMdd-HHmmss')}"
        // echo "Generated Engagement Name: ${engagementName}"
        // Store the engagementName in an environment variable
        // env.ENGAGEMENT_NAME = engagementName
        // def engagementName = "Engagement-${BUILD_ID}"
        // echo "Generated Engagement Name: ${engagementName}"
        // Use 'engagementName' further in your pipelined
        // def curlCommand = "curl -X POST -d 'engagement=${env.ENGAGEMENT_NAME}' http://example.com/api"
        def curlCommand = "curl -X 'POST' \
        'https://defectdojo.dalmiabharat.com/api/v2/reimport-scan/' \
        -H 'accept: application/json' \
        -H 'Authorization: Token 212983a2789afcd09f252a66d83b46a8fa4a8c39' \
        -H 'Content-Type: multipart/form-data' \
        -H 'X-CSRFTOKEN: agVi7AHZPZ13PBfCOABb4yn6v12KIUNoLvf34b9vNHS0X2qig1Exvd6J0Nnkw7YO' \
        -F 'active=true' \
        -F 'do_not_reactivate=false' \
        -F 'verified=true' \
        -F 'close_old_findings=true' \
        -F 'engagement_name=${env.ENGAGEMENT_NAME}' \
        -F 'push_to_jira=false' \
        -F 'minimum_severity=Info' \
        -F 'close_old_findings_product_scope=false' \
        -F 'create_finding_groups_for_all_findings=true' \
        -F 'tags=mobsf' \
        -F 'product_name=Product-II' \
        -F 'file=@mobsfscan.json;type=application/json' \
        -F 'auto_create_context=true' \
        -F 'scan_type=Mobsfscan Scan'"
        sh curlCommand
        // sh '''
        // curl -X 'POST' \
        // 'https://defectdojo.dalmiabharat.com/api/v2/reimport-scan/' \
        // -H 'accept: application/json' \
        // -H 'Authorization: Token 212983a2789afcd09f252a66d83b46a8fa4a8c39' \
        // -H 'Content-Type: multipart/form-data' \
        // -H 'X-CSRFTOKEN: agVi7AHZPZ13PBfCOABb4yn6v12KIUNoLvf34b9vNHS0X2qig1Exvd6J0Nnkw7YO' \
        // -F 'active=true' \
        // -F 'do_not_reactivate=false' \
        // -F 'verified=true' \
        // -F 'close_old_findings=true' \
        // -F 'engagement_name=${env.ENGAGEMENT_NAME}' \
        // -F 'push_to_jira=false' \
        // -F 'minimum_severity=Info' \
        // -F 'close_old_findings_product_scope=false' \
        // -F 'create_finding_groups_for_all_findings=true' \
        // -F 'tags=mobsf' \
        // -F 'product_name=Product-II' \
        // -F 'file=@mobsfscan.json;type=application/json' \
        // -F 'auto_create_context=true' \
        // -F 'scan_type=Mobsfscan Scan' 
        // '''
        }
      }      
    }
  }
}
