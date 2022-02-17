pipeline {
    agent any 
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', credentialsId: '7d45d4df-5f8a-49e0-af51-c0f629e77c4b', url: 'https://github.com/ThuyLam999/BackEnd.git'
            }
        }
        
        stage('Restore packages'){
            steps{
                bat "dotnet restore web-api/web-api/web-api.csproj"
            }
        }

        stage('Clean'){
            steps{
                bat "dotnet clean web-api/web-api/web-api.csproj"
            }
        }

        stage('Build'){
            steps{
                bat "dotnet build web-api/web-api/web-api.csproj --configuration Release --no-restore"
            }
        }

        stage('Test: Unit Test'){
            steps {
                bat 'dotnet test web-api/web-api-tests/web-api-tests.csproj --configuration Release --no-restore'
            }
        }
       
        stage('Test: Integration Test'){
            steps {
                 echo 'Test: Integration Test'
            }
        }
    }
    post {
        always {
            cleanWs()
        }
        
        success {
            mail bcc: '', body: 'Thông báo kết quả build', cc: '', from: '', replyTo: '', subject: 'Test Run SUCCESSFUL', to: 'thanhthuyyasou234@gmail.com'
        }  

        failure {
            mail bcc: '', body: 'Thông báo kết quả build', cc: '', from: '', replyTo: '', subject: 'Test Run FAILED', to: 'thanhthuyyasou234@gmail.com'
        }
    }
}
