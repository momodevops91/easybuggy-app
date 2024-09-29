pipeline{
    agent any
    tools{
        maven 'maven'
    }
    stages{
        stage('CompileandRunSonarAnalysis'){
            steps{
                withCredentials([string(credentialsId: 'sonarcloudinfo', variable: 'tech365token')]) {
                    sh 'mvn clean verify sonar:sonar -Dsonar.login=$tech365token -Dsonar.organization=tech365 -Dsonar.host.url=https://sonarcloud.io -Dsonar.projectKey=tech365key'
                    
                }
            }
        }
       

    }
}