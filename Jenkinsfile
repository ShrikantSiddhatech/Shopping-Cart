pipeline {
    agent any
    
    options {
        disableConcurrentBuilds()
    }


    stages {
        stage('Katalon TC') {
            steps {
                lock(resource: 'my_lock') {
                    script{
                        try{
                            sh '''
                            cd /Users/aditidixit/Downloads/KRE.app/Contents/MacOS
                            ./katalonc -noSplash -runMode=console \
                            -projectPath="/Users/aditidixit/Documents/Shopping-Cart/shopping-cart-tests.prj" \
                            -retry=0 \
                            -testSuitePath="Test Suites/TS_1" \
                            -browserType="Chrome" \
                            -executionProfile="default" \
                            -apiKey="a7e45f80-496e-47da-9d8d-09cca7cac63f" \
                            '''

                            if (result != 0) {
                                throw new Exception("Katalon tests failed with exit code ${result}")
                            }

                        }catch(Exception e){
                            emailext (
                            subject: "${env.JOB_NAME} - Build #${env.BUILD_NUMBER}",
                            body: "The build was Faild! Please Check : ${env.BUILD_URL}",
                            to: 'siddhaappempresa2@gmail.com'
                            )        
                        } 
                    }
                }       
            }
        }

    }

    post {
        always {
            script {
                emailext(
                    subject: "Build Status",
                    body: "The build was Success, Please Check : ${env.BUILD_URL}",
                    attachLog: true,
                    recipientProviders: [[$class: 'CulpritsRecipientProvider'], [$class: 'DevelopersRecipientProvider']],
                    to: 'siddhaappempresa2@gmail.com'
                )
            }

            echo 'Cleaning Workspace'
            cleanWs()
       }
    }


}
