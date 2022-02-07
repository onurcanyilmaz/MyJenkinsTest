pipeline{
    agent any
    
    environment {
        dotnet ='C:\\Program Files (x86)\\dotnet\\'
        }
        
    triggers {
        pollSCM 'H * * * *'
    }
	
	stages{
	stage('Checkout') {
    steps {
    url: 'https://github.com/onurcanyilmaz/MyJenkinsTest.git', branch: 'master'
     }
  }
  
  stage('Restore packages'){
   steps{
      bat "dotnet restore MyJenkinsTest\\MyJenkinsTest.csproj"
     }
  }
  
  stage('Clean'){
    steps{
        bat "dotnet clean MyJenkinsTest\\MyJenkinsTest.csproj"
     }
   }
   
   stage('Build'){
   steps{
      bat "dotnet build MyJenkinsTest\\MyJenkinsTest.csproj --configuration Release"
    }
 }
 
 stage('Test: Unit Test'){
   steps {
     bat "dotnet test MyJenkinsTest\\MyJenkinsTest.NUnitTestProject\\MyJenkinsTest.NUnitTestProject.csproj"
     }
  }

   stage('Publish'){
     steps{
       bat "dotnet publish YourProjectPath\\Your_Project.csproj "
     }
}
 }
 }