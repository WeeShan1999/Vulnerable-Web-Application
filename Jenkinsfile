pipeline {
    agent any
    stages {
        stage ('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/WeeShan1999/Vulnerable-Web-Application.git'
            }
        }
        stage('Code Quality Check via SonarQube') {
            steps {
                script {
                    def scannerHome = tool 'SonarQube';
                    withSonarQubeEnv('SonarQube') {
                        sh """
                            ${scannerHome}/bin/sonar-scanner 
                            -Dsonar.projectKey=OWASP 
                            -Dsonar.sources=. 
                            -Dsonar.host.url=http://172.18.0.4:9000 
                            -Dsonar.token=sqp_0f2b0a570d88ef57f570ed18eea898ce60417510
                        """
                    }
                }
            }
        }
    }
    post {
        always {
            recordIssues enabledForFailure: true, tool: sonarQube()
        }
    }
}
