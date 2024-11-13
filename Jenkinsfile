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
        stage('osv-scanner') {
            steps {
                sh 'osv-scanner scan --lockfile package-lock.json --json --output results/osv-report.json || true'               
            }
        }
      #  post {
       #     always {
        #        defectDojoPublisher(artifact: 'results/sca-osv-scanner.json', 
       #             productName: 'Juice Shop', 
      #              scanType: 'OSV Scan', 
      #              engagementName: 'marcin.mazurek@merito.pl')
       #     }
     #   }
    }
}
