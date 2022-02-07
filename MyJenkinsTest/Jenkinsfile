pipeline {
    agent any
    environment {
        PROJECT_NAME = "MyJenkinsTest"
        PROJECT_URL = "https://github.com/onurcanyilmaz/MyJenkinsTest"
        DOTNET ="C:\Program Files\dotnet\dotnet.exe"
        COVERLET_OUTPUT_PATH = "coverlet-output-path"
        SONAR_SCANNER ="sonar-scanner-path"
        SONARQUBE_HOST_URL = "http://localhost:9000"
        SONARQUBE_TOKEN = "eecc3a5f4f1828dc744ae2af783a6ae446bec8c6"
        PROJECT_FILE_PATH ="MyJenkinsTest/MyJenkinsTest.csproj"
        TEST_PROJECT_FILE_PATH="MyJenkinsTest.NUnitTestProject/MyJenkinsTest.NUnitTestProject.csproj"
    }
    stages {
        stage('Checkout') {
            steps {
                git(
                    url:"${PROJECT_URL}"
                )
            }
        }
        stage('Restore Packages') {
            steps {
                sh "${DOTNET} restore"
            }
        }
        stage('Clean Project') {
            steps {
                sh "${DOTNET} clean"
            }
        }
        stage('Build Project') {
            steps {
                sh "${DOTNET} build"
            }
        }
        stage('Run Tests') {
            steps {
                sh "${DOTNET} test"
            }
        }
        stage('Run Test Coverage') {
            steps {
                sh "${DOTNET} test --no-restore --no-build ${TEST_PROJECT_FILE_PATH} /p:CollectCoverage=true /p:CoverletOutputFormat=opencover /p:CoverletOutput=\"${COVERLET_OUTPUT_PATH}\""
                sh "${SONAR_SCANNER} begin /k:\"${PROJECT_NAME}\" /d:sonar.host.url=\"${SONARQUBE_HOST_URL}\" /d:sonar.login=\"${SONARQUBE_TOKEN}\" /d:sonar.cs.opencover.reportsPaths=\"${COVERLET_OUTPUT_PATH}.opencover.xml\""
                sh "${DOTNET} build"
                sh "${SONAR_SCANNER} end /d:sonar.login=\"${SONARQUBE_TOKEN}\""
            }
        }
    }
}