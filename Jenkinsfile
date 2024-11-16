pipeline {
    agent any
    options {
        skipDefaultCheckout(true)
    }
    stages {
        stage('Code checkout from GitHub') {
            steps {
                script {
                    cleanWs()
                    git credentialsId: 'github-token', url: 'https://github.com/mmer383/abcd-student', branch: 'main'
                }
            }
        }
      //  stage('osv-scanner') {
      //      steps {
      //          sh 'mkdir -p results/'  
     //           sh 'osv-scanner scan --lockfile package-lock.json --json --output results/osv-report.json || true'   
     //           sh 'cat "${WORKSPACE}/results/osv-report.json"'
    //        }
         //  post {
           //    always {
             //   defectDojoPublisher(artifact: '${WORKSPACE}/results/osv-report.json', 
               //     productName: 'Juice Shop', 
                 //   scanType: 'OSV Scan', 
                   // engagementName: 'marcin.mazurek@merito.pl')
              // }
           // }
        //}
        //stage('trufflehog') {
        //    steps {
        //        sh 'mkdir -p results/'  
                // sh 'trufflehog git file://. --branch main --json --only-verified --force-skip-archives > "${WORKSPACE}/results/trufflehog_result.json" || true'
         //       sh 'trufflehog git file://. --branch main --json --force-skip-archives > "${WORKSPACE}/results/trufflehog_result.json" || true'
         //       sh 'cat "${WORKSPACE}/results/trufflehog_result.json"'
         //   }
         //   post {
          //     always {
          //      defectDojoPublisher(artifact: '${WORKSPACE}/results/trufflehog_result.json', 
          //          productName: 'Juice Shop', 
          //          scanType: 'Trufflehog Scan', 
          //          engagementName: 'marcin.mazurek@merito.pl')
          //     }
          // }
        //}
  //        stage('semgrep') {
  //          steps {
  //              sh 'mkdir -p results/'  
  //              sh 'semgrep --config auto --json --output "${WORKSPACE}/results/semgrep_result.json" || true'
  //              sh 'cat "${WORKSPACE}/results/semgrep_result.json"'
  //          }
  //          post {
   //            always {
  //             defectDojoPublisher(artifact: '${WORKSPACE}/results/semgrep_result.json', 
   //                 productName: 'Juice Shop', 
  //                  scanType: 'Semgrep JSON Report', 
  //                  engagementName: 'marcin.mazurek@merito.pl')
  //             }
  //         }
  //      }
        stage('[ZAP] Baseline passive-scan') {
            steps {
                sh 'mkdir -p results/'
                sh '''
                    docker run --name juice-shop -d --rm -p 3000:3000 bkimminich/juice-shop
                    sleep 15
                '''
                sh '''
                    docker run --name zap --add-host=host.docker.internal:host-gateway \
                    -v /home/mm/abcd/abcd-lab/zap:/zap/wrk/:rw \
                    -t ghcr.io/zaproxy/zaproxy:stable bash -c \
                    "zap.sh -cmd -addonupdate; zap.sh -cmd -addoninstall communityScripts -addoninstall pscanrulesAlpha -addoninstall pscanrulesBeta -autorun /zap/wrk/passive_scan.yaml" \
                    || true'''
            }
            post {
                success {
                    sh '''
                    docker cp zap:/zap/wrk/reports/zap_html_report.html ${WORKSPACE}/results/zap_html_report.html
                    docker cp zap:/zap/wrk/reports/zap_xml_report.xml ${WORKSPACE}/results/zap_xml_report.xml
                    cat "${WORKSPACE}/results/zap_xml_report.xml"
                    docker stop zap juice-shop || true
                    docker rm zap
                    '''
                }
                failure {
                    sh '''
                    docker stop zap juice-shop || true
                    docker rm zap
                    '''
                }
            }
        }

        
        
     //   stage('zap scan') {
     //       steps {
     //           sh 'mkdir -p results/'  
     //           sh 'semgrep --config auto --json --output "${WORKSPACE}/results/semgrep_result.json" || true'
     //           sh 'cat "${WORKSPACE}/results/semgrep_result.json"'
     //       }
     //       post {
    //           always {
    //           defectDojoPublisher(artifact: '${WORKSPACE}/results/semgrep_result.json', 
     //               productName: 'Juice Shop', 
    //                scanType: 'ZAP Scan', 
    //                engagementName: 'marcin.mazurek@merito.pl')
    //           }
    //       }
        }
   // }
}
