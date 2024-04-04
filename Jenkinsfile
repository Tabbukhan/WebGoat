pipeline {
  agent any
    environment {
        GITGUARDIAN_API_KEY = credentials('guardian-token')
    }
  stages {
    stage('TruffleHog Scan') {
            steps {
                // Run TruffleHog scan
                sh 'trufflehog --regex --entropy=True .'
            }  
    }
    stage('Scan with GitGuardian') {
      steps {
          // Run GitGuardian scan with API key
                sh "ggsync scan --api-key ${GITGUARDIAN_API_KEY}"
          
        // withCredentials([string(credentialsId: 'gitguardian-api-key', variable: 'GITGUARDIAN_API_KEY')]) {
         // sh 'ggshield secret scan ci'
        }
      }
    //stage('scan') {
            //steps {
           // sh "docker run -v ${WORKSPACE}:/src --workdir /src returntocorp/semgrep-agent:v1 semgrep-agent --config p/ci --config p/security-audit --config p/secrets"
           // }
   // }
  }
}
