pipeline {
    agent any
    
    stages {
        stage('Create Engagement') {
            steps {
                script {
                    def buildNumber = currentBuild.getNumber()
                    def timestamp = new Date().format("dd-MM-yyyy_HH:mm:ss", TimeZone.getTimeZone("Asia/Kolkata"))
                    def engagementName = "Engagement_${buildNumber}_${timestamp}"

                    echo "Engagement Name: ${engagementName}"
                    
                    // Use the engagementName in your curl command
                    // sh "curl -X POST -d 'engagement=${engagementName}' http://your-api-endpoint"
                }
            }
        }
    }
}
