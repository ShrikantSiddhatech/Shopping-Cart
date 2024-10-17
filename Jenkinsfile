pipeline {
    agent any
    
    options {
        disableConcurrentBuilds()
    }


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
                        -reportFolder='/Users/aditidixit/Documents/Shopping-Cart/Reports'
                    '''    
            }
        }

        // stage('Archive Reports') {
        //     steps {
        //         archiveArtifacts artifacts: '/Users/aditidixit/Documents/Shopping-Cart/Reports/report.html', allowEmptyArchive: true
        //     }
        // }

    }

    post {
        always {
            script {
                emailext(
                subject: "Katalon Test Report",
                body: "Please find the attached Katalon test report.",
                attachLog: true,
                attachments: '/Users/aditidixit/Documents/Shopping-Cart/Reports/report.html',               
                recipientProviders: [[$class: 'CulpritsRecipientProvider'], [$class: 'DevelopersRecipientProvider']],
                to: 'siddhaappempresa2@gmail.com'
               )
            }
        
            // publishHTML(target: [
            //   reportDir: '/Users/aditidixit/Documents/Shopping-Cart/Reports',
            //   reportFiles: 'report.html',
            //   reportName: 'Katalon Test Report',
            //   keepAll: true,
            //   alwaysLinkToLastBuild: true
            // ])
       }
    }


}
