pipeline{

agent any

environment {
dotnet = 'C:\\Program Files (x86)\\dotnet\\'
}

triggers {
    pollSCM 'H * * * *'
}

stages {
    stage('Checkout') {
      steps {
        git credentialsId: '', url: 'https://github.com/onurcanyilmaz/MyJenkinsTest.git', branch: 'master'
      }
    }

    stage('Restore packages') {
      steps {
        bat "dotnet restore MyJenkinsTest\\MyJenkinsTest.csproj"
      }
    }

    stage('Clean') {
      steps {
        bat "dotnet clean MyJenkinsTest\\MyJenkinsTest.csproj"
      }
    }

    stage('Build') {
      steps {
        bat "dotnet build MyJenkinsTest\\MyJenkinsTest.csproj --configuration Release"
      }
    }

    stage('Test: Unit Test') {
      steps {
        bat "dotnet test MyJenkinsTest.NUnitTestProject\\MyJenkinsTest.NUnitTestProject.csproj"
      }
    }

    stage('Publish') {
      steps {
        bat "dotnet publish MyJenkinsTest\\MyJenkinsTest.csproj"
      }
    }
  }

 post {
    always {
      echo 'This will always run'
    }
    success {
      echo 'This will run only if successful'
    }
    failure {
      echo 'hata alındı'
    }
    unstable {
      echo 'This will run only if the run was marked as unstable'
    }
    changed {
      echo 'This will run only if the state of the Pipeline has changed'
      echo 'For example, if the Pipeline was previously failing but is now successful'
    }
  }

}