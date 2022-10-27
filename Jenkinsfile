pipeline {
    agent {
        kubernetes {
            defaultContainer 'jnlp'
            yaml libraryResource("podTemplates/aws.yaml")
        }
    }

    stages {
        stage('List EKS clusters') {
            steps {
                container('awscli') {
                    withAWS(role:"${ROLE_TO_ASSUME}", roleAccount:"${ACCEPTANCE_ACCOUNT_ID}", externalId: "${ROLE_EXTERNAL_ID}", duration: "${ASSUME_DURATION}", roleSessionName: "${ROLE_SESSION_NAME}", region:"${AWS_REGION}") {
                        sh 'aws eks list-clusters'
                    }
                }
            }
        }
    }
}
