pipeline {
    agent none 

    stages {
        stage('Dotnet') {
            agent{docker{image 'mcr.microsoft.com/dotnet/sdk:6.0'}}
            steps {
                sh 'dotnet build'
                sh 'dotnet test'
            }
            environment{ 
                DOTNET_CLI_HOME = '/tmp/dotnet_cli_home'
    
            }
        }
        stage('node') {
            agent{docker{image 'node:17-bullseye'}}
            steps {
                dir ('DotnetTemplate.Web'){
                    sh 'npm install'
                    sh 'npm run build'
                    sh 'npm t'
                    sh 'npm run lint'
                }
            
            }
        }
        
    }
}