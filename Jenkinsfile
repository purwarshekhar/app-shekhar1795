pipeline {
  agent any

  environment {
    scannerHome = 'sonar_scanner_dotnet'
    username = 'shekharpurwar'
    appName = 'Helloworld'
  }

  options {

    timestamps()
  
    buildDiscarder(logRotator(
      // number of build logs to keep
      numToKeepStr: '10',
      // Days to keep histry 
      daysToKeepStr: '30'
    ))
  }

  stages {

   
    
   
    

     stage('Kubernetes Deployment') {
       
       steps{
          echo "Start deplying deplyment.yaml file"
          powershell '''(Get-Content deployment.yaml).replace('[BranchName]','${BRANCH_NAME}') | Set-Content deployment.yaml'''
           bat "kubectl apply -f deployment.yaml"
          echo "Start deplying serice.yaml file"
          bat "kubectl apply -f service.yaml"
      }
    }
  }

  post {
    always {
      echo 'Workspace Cleanup'
      
    }
  }
}
