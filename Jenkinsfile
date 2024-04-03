pipeline {
  agent any
  stages {
    stage('TruffleHog Scan') {
            steps {
                // Run TruffleHog scan
                sh 'trufflehog --regex --entropy=True .'
            }  
    }
    stage('Gitleaks Scan') {
            steps {
                // Run Gitleaks scan
                sh 'gitleaks --verbose --repo-path .'
            }
    }
    stage('scan') {
            steps {
            sh "docker run -v ${WORKSPACE}:/src --workdir /src returntocorp/semgrep-agent:v1 semgrep-agent --config p/ci --config p/security-audit --config p/secrets"
            }
    }
  }
}
