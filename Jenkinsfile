pipeline {
  agent any
  stages {
    stage('TruffleHog Scan') {
            steps {
                // Run TruffleHog scan
                sh 'trufflehog --regex --entropy=True .'
            }  
    }
      stage('GitGuardian Scan') {
            environment {
                GITGUARDIAN_API_KEY = credentials('guardian-token')
            }
            steps {
                sh 'ggshield secret scan ci'
            }
        }
      stage('Semgrep-Scan') {
          environment {
      // The following variable is required for a Semgrep Cloud Platform-connected scan:
      SEMGREP_APP_TOKEN = credentials('SEMGREP_APP_TOKEN')
          }
        steps {
          sh 'pip3 install semgrep'
          sh 'semgrep ci'
     }
    }
      
      
    //stage('Scan with GitGuardian') {
     // steps {
          // Run GitGuardian scan with API key
             //   sh "ggsync scan --api-key ${GITGUARDIAN_API_KEY}"
          
        // withCredentials([string(credentialsId: 'gitguardian-api-key', variable: 'GITGUARDIAN_API_KEY')]) {
         // sh 'ggshield secret scan ci'
       // }
      //}
    //stage('scan') {
            //steps {
           // sh "docker run -v ${WORKSPACE}:/src --workdir /src returntocorp/semgrep-agent:v1 semgrep-agent --config p/ci --config p/security-audit --config p/secrets"
           // }
   // }
  }
}
