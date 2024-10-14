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
                        -apiKey="a7e45f80-496e-47da-9d8d-09cca7cac63f"
                    '''    
            }
        }
    }

    post {
        always {
            script {
                // Send email notification
                emailext(
                    subject: "Build ${currentBuild.fullDisplayName} - ${currentBuild.currentResult}",
                    body: """<p>Build ${currentBuild.fullDisplayName} finished with status: ${currentBuild.currentResult}</p>""",
                    to: 'shrikantd@siddhatech.com',
                    mimeType: 'text/html'
                )
            }
        }
    }

}
