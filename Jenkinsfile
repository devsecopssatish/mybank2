pipeline {
    agent any 
    stages {
        stage('Secrest scanning') {
            steps {
                sh """
                   gitleaks detect . -v --redact -f json -r secrets-scanning-report.json
                """
            }
             post {
                always {
                    archiveArtifacts artifacts: "secrets-scanning-report.json" , allowEmptyArchive: true
                }
            }

        } //end secrets scanning

        stage('Trivy SCA') {
            steps {
                sh """
                    echo "This is SCA"
                """
            }
        } //end snyk sca

    } //end stages
} // end pipeline
