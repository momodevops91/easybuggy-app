pipeline {
  agent any
  tools { 
        maven 'Maven_3_5_2'  
    }
   stages{

    // sonar analysis

    stage('CompileandRunSonarAnalysis') {
            steps {	
		sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=tech365app -Dsonar.organization=tech365app -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=26744a8c3cb27f934e110753eb99af5070e61c7e'
			}
    }

// snyk analisys
	stage('RunSCAAnalysisUsingSnyk') {
            steps {		
				withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
					sh 'mvn snyk:test -fn'
				}
			}
    }	

// building docker image
	stage('Build') { 
            steps { 
               withDockerRegistry([credentialsId: "dockerlogin", url: ""]) {
                 script{
                 app =  docker.build("tech365image")
                 }
               }
            }
    }

	stage('Push') {
            steps {
                script{
                    docker.withRegistry('https://924338258393.dkr.ecr.us-east-2.amazonaws.com', 'ecr:us-east-2:aws-credentials') {
                    app.push("latest")
                    }
                }
            }
    	}

    // deploy to kubernetes cluster

    stage('Kubernetes Deployment of Easy Buggy Web Application') {
	   steps {
	      withKubeConfig([credentialsId: 'kubelogin']) {
		  sh('kubectl delete all --all -n devsecops')
		  sh ('kubectl apply -f deployment.yaml --namespace=devsecops')
		}
	      }
   	}
	    
  }
}
