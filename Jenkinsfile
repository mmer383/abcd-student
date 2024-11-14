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
                  stage('zap scan') {
            steps {
                sh 'mkdir -p results/'  
                sh 'semgrep --config auto --json --output "${WORKSPACE}/results/semgrep_result.json" || true'
                sh 'cat "${WORKSPACE}/results/semgrep_result.json"'
            }
     //       post {
    //           always {
    //           defectDojoPublisher(artifact: '${WORKSPACE}/results/semgrep_result.json', 
     //               productName: 'Juice Shop', 
    //                scanType: 'ZAP Scan', 
    //                engagementName: 'marcin.mazurek@merito.pl')
    //           }
    //       }
        }
    }
}
