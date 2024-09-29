pipeline{
    agent any
    tools{
        maven 'maven'
    }
    stages{
        stage('CompileandRunSonarAnalysis'){
            steps{
                withCredentials([string(credentialsId: 'sonarcloudinfo', variable: 'sonarcloudinfo')]) {
                    sh 'mvn clean verify sonar:sonar -Dsonar.login=$sonarcloudinfo -Dsonar.organization=tech365 -Dsonar.host.url=https://sonarcloud.io -Dsonar.projectKey=tech365key'
                    
                }
            }
        }
       

    }
}