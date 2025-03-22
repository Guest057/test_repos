pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                bat '"C:\\Users\\Green\\Desktop\\pusta_papka\\nuget.exe" restore test_repos.sln'
                bat '"C:\\Program Files\\Microsoft Visual Studio\\2022\\Community\\MSBuild\\Current\\Bin\\MSBuild.exe" test_repos.sln /t:Build /p:Configuration=Release /p:RestorePackagesConfig=true'
            }
        }
        
        stage('Test') {
            steps {
                bat "x64\\Release\\test_repos.exe --gtest_output=xml:test_report.xml"
            }
        }
    }
    
    post {
        always {
            xunit (tools: [ GoogleTest(pattern: 'test_report.xml') ], skipPublishingChecks: false)
        }
    }
}