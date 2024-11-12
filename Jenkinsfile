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
                sh osv-scanner scan --lockfile package-lock.json --json --output /var/jenkins_home/workspace/ABCD pipeine/results/osv-report.json                
            }
        }
    }
}
