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

        // stage('List Workspace') {
        //     steps {
        //         sh 'ls -R' // This will list all files and directories in the workspace
        //     }
        // }

        stage('Archive Reports') {
            steps {
                archiveArtifacts artifacts: '/Users/aditidixit/Documents/Shopping-Cart/Reports/*.html', allowEmptyArchive: true
            }
        }

        // stage('List Reports Directory') {
        //     steps {
        //         sh 'ls -R "/Users/aditidixit/Downloads/KRE.app/Contents/MacOS/Reports" || echo "No Reports folder found"'
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
                recipientProviders: [[$class: 'CulpritsRecipientProvider'], [$class: 'DevelopersRecipientProvider']],
                to: 'siddhaappempresa2@gmail.com'
               )
            }
        
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
