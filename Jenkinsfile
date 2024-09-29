pipeline{
    agent any
    tools{
        maven 'maven'
    }
    stages{
        // sonarcloud analysis
        stage('CompileandRunSonarAnalysis'){
            steps{
                withCredentials([string(credentialsId: 'tech365token', variable: 'tech365token')]) {
                    sh 'mvn clean verify sonar:sonar -Dsonar.login=$tech365token -Dsonar.organization=tech365 -Dsonar.host.url=https://sonarcloud.io -Dsonar.projectKey=tech365'
                    
                }
            }
        }

        // snyk code analysis
        stage('RunSnykCodeAnalysis'){
        steps{
            withCredentials([string(credentialsIs:'snyk_token', variable: 'snyk_token')]) {
                sh 'mvn snyk:test -fn'
            }
        }
        }
       

    }
}