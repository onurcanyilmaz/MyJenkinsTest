pipeline {
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
	
	stage('Building our image') {
	 steps{
		script {
				dockerImage = docker.build registry + ":$BUILD_NUMBER"
			}
		}
	}
  }
  post {
    always {
      echo 'The pipeline was started'
    }
    success {
	  //mail bcc: '', body: "<b>Deployment Status:</b><br>Project: ${env.JOB_NAME} <br>Build Number: ${env.BUILD_NUMBER} <br> URL build: ${env.BUILD_URL}", cc: '', charset: 'UTF-8', from: '', mimeType: 'text/html', replyTo: '', subject: "SUCCESS CI: Project name -> ${env.JOB_NAME}", to: 'onurcan.yilmaz@sensormatic.com.tr'
      echo 'The pipeline was succeeded'
    }
    failure {
      mail bcc: '', body: "<b>Deployment Status:</b><br>Project: ${env.JOB_NAME} <br>Build Number: ${env.BUILD_NUMBER} <br> URL build: ${env.BUILD_URL}", cc: '', charset: 'UTF-8', from: '', mimeType: 'text/html', replyTo: '', subject: "ERROR CI: Project name -> ${env.JOB_NAME}", to: 'onurcan.yilmaz@sensormatic.com.tr'
    }
    unstable {
      echo 'The pipeline was marked as unstable'
    }
    changed {
      echo 'The Pipeline has changed'
    }
  }
}
