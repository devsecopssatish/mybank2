pipeline {
    agent any 
    stages {
        stage('Secrest scanning') {
            steps {
                sh """
                    echo "This is secrets scanning"
                """
            }
        } //end secrets scanning

        stage('Snyk SCA') {
            steps {
                sh """
                    echo "This is SCA"
                """
            }
        } //end snyk sca

    } //end stages
} // end pipeline
