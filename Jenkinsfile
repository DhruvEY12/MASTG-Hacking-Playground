pipeline {
    agent any
    
    stages {
        stage('MobSF-Scan') {
      steps {
        sh 'mobsfscan iOS/MSTG-JWT/ --json -o mobsfscan.json'
      }
    }
        stage('Create Engagement') {
            steps {
                script {
                    def buildNumber = currentBuild.getNumber()
                    def engagementId = buildNumber.toString()
                    // def timestamp = new Date().format("dd-MM-yyyy_HH:mm:ss", TimeZone.getTimeZone("Asia/Kolkata"))
                    // def engagementName = "Engagement-${buildNumber}_Timestamp-${timestamp}"

                    // echo "Engagement Name: ${engagementName}"
                    echo "Engagement ID: ${engagementId}"
                    
                    // Use the engagementName in your curl command
                    // sh "curl -X POST -d 'engagement=${engagementName}' http://your-api-endpoint"
                       sh "curl -X 'POST' \
                        'https://defectdojo.dalmiabharat.com/api/v2/reimport-scan/' \
                        -H 'accept: application/json' \
                        -H 'Authorization: Token 212983a2789afcd09f252a66d83b46a8fa4a8c39' \
                        -H 'Content-Type: multipart/form-data' \
                        -H 'X-CSRFTOKEN: agVi7AHZPZ13PBfCOABb4yn6v12KIUNoLvf34b9vNHS0X2qig1Exvd6J0Nnkw7YO' \
                        -F 'active=true' \
                        -F 'do_not_reactivate=false' \
                        -F 'verified=true' \
                        -F 'close_old_findings=true' \
                        // -F 'engagement=${engagementName}' \
                        -F 'engagement=${engagementId}' \
                        -F 'push_to_jira=false' \
                        -F 'minimum_severity=Info' \
                        -F 'close_old_findings_product_scope=false' \
                        -F 'create_finding_groups_for_all_findings=true' \
                        -F 'tags=mobsf' \
                        -F 'product_name=Product-II' \
                        -F 'file=@mobsfscan.json;type=application/json' \
                        -F 'auto_create_context=true' \
                        -F 'scan_type=Mobsfscan Scan'"
                    }
                }
            }
        }
    }
