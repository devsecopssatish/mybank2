pipeline {
    agent any 
    stages {
        stage('Secrest scanning') {
            steps {
				catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                sh """
                   gitleaks detect . -v --redact -f json -r secrets-scanning-report.json
                """
				}
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



		stage('snyk Scanning - sast') {
			        environment {
	    	SNYK_TOKEN = credentials('SNYK_TOKEN')
	    }
            steps {
		
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                sh '''
					echo $SNYK_TOKEN
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
