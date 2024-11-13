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
                sh 'mkdir -p results/'  
                sh 'osv-scanner scan --lockfile package-lock.json --json --output results/osv-report.json || true'               
            }
        }

    }
}
