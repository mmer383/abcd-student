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
        stage('trufflehog') {
            steps {
                sh 'mkdir -p results/'  
                sh 'trufflehog git file://. --branch main --json --only-verified --force-skip-archives > "${WORKSPACE}/results/trufflehog_result.json" || true'   
                sh 'cat "${WORKSPACE}/results/trufflehog_result.json"'
            }
          // post {
          //     always {
          //      defectDojoPublisher(artifact: '${WORKSPACE}/results/osv-report.json', 
          //          productName: 'Juice Shop', 
          //          scanType: 'OSV Scan', 
          //          engagementName: 'marcin.mazurek@merito.pl')
          //     }
          //  }
        }
    }
}
