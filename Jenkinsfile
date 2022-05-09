pipeline { 
   agent { 
       docker { 
           image 'mcr.microsoft.com/dotnet/sdk:6.0' 
       } 
   } 
   environment { 
       DOTNET_CLI_HOME = "/tmp/DOTNET_CLI_HOME" 
   } 
   stages { 
       stage('Restore packages') { 
          steps { 
             sh 'dotnet restore WebApplication.sln' 
          } 
       } 
       stage('Clean') { 
          steps { 
               sh 'dotnet clean WebApplication.sln --configuration Release' 
          } 
       } 
 
 stage('Test: Unit Test') { 
    steps { 
        sh 'dotnet test XUnitTestProject/XUnitTestProject.csproj --configuration Release --no-restore' 
      }
    }
 
    stage('Build') { 
       steps { 
          sh 'dotnet build WebApplication.sln --configuration Release --no-restore' 
          } 
       }
    stage('Publish') { 
       steps { 
           sh 'dotnet test XUnitTestProject/XUnitTestProject.csproj --configuration Release --no-restore' 
          }
    }
    stage('Archive') { 
       steps { 
           sh 'tar -cvzf publish.tar.gz --strip-components=1 WebApplication/bin/Release/netcoreapp3.1/publish' 
           archive 'publish.tar.gz' 
          } 
       }
    
   stage('Nexus Upload Stage') {
     agent none 
     steps { 
       sh 'ls'
       } 
   } 

    stage('Deploy Stage') {
      steps { 
      sh 'ls -a'
     
    }
   }
  }
}
