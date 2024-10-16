pipeline {
    agent any
    
    stages {
        stage('Katalon TC') {
            steps {
                sh '''
                    cd /Users/aditidixit/Downloads/KRE.app/Contents/MacOS
                    ./katalonc -noSplash -runMode=console \
                        -projectPath="/Users/aditidixit/Documents/Shopping-Cart/shopping-cart-tests.prj" \
                        -retry=0 \
                        -testSuitePath="Test Suites/TS_1" \
                        -browserType="Chrome" \
                        -executionProfile="default" \
                        -apiKey="a7e45f80-496e-47da-9d8d-09cca7cac63f" \
                        -reportFolder='Reports'
                        -reportFile="Report"
                    '''    
            }
        }
        
        stage('Archive Reports') {
            steps {
                archiveArtifacts artifacts: 'Reports/*.html', allowEmptyArchive: true
            }
        }
    }

    post {
    always {
        script {
            emailext(
                subject: "Katalon Test Report",
                body: "Please find the attached Katalon test report.",
                attachLog: true,
                recipientProviders: [[$class: 'CulpritsRecipientProvider'], [$class: 'DevelopersRecipientProvider']],
                to: 'shrikantd@siddhatech.com'
            )
        }

        // Move publishHTML outside of the script block
        publishHTML(target: [
            reportDir: 'Reports',
            reportFiles: 'Report.html', // Ensure this matches your report file name
            reportName: 'Katalon Test Report',
            keepAll: true,
            alwaysLinkToLastBuild: true
        ])
    }
}


}
