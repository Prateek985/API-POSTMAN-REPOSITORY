pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo("build the war")
            }
        }
        stage("Deploy to QA") {
            steps {
                echo("deploy to QA")
            }
        }
        stage("Checkout") {
            steps {
                git url: 'https://github.com/Prateek985/API-POSTMAN-REPOSITORY.git'            
             }
        }
        stage('Run api test cases') {
            steps {
                bat 'mkdir results'
                bat """
                    newman run "Booking_APIsWorkFlowCollection.json" ^
                        -e "Booking_API_Enviroment.json" ^
                        -r cli,htmlextra ^
                        --reporter-htmlextra-export "./results/Booking_report.html"
                """
            }
        }
       stage('Publish HTML Extra Report') {
            steps {
                     publishHTML([allowMissing: false,
                                  alwaysLinkToLastBuild: false,
                                  keepAll: true,
                                  reportDir: 'results',
                                  reportFiles: 'Booking_report.html',
                                  reportName: 'HTML Extra API Report',
                                  reportTitles: ''])
            }
        }
       stage("Deploy to PROD") {
            steps {
                echo("deploy to PROD")
            }
        }
    }  
}