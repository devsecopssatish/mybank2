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


        environment {
	    	SNYK_TOKEN = credentials('SNYK_TOKEN')
	    }
		stage('snyk Scanning - sast') {
            steps {
		
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                sh '''
					snyk auth $SNYK_TOKEN
					snyk code test -o snyk-sast.html
                '''
                }
            }
            post {
                always {
                    archiveArtifacts artifacts: "snyk-sast.html" , allowEmptyArchive: true
                }
            }
        }

    } //end stages
} // end pipeline
