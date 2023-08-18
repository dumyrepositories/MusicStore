pipeline {
    agent { label ('Dotnet6') }
    triggers { pollSCM ('H/5 * * * *')}
    stages {
        stage('vcs') {
            steps {
                git url: 'https://github.com/dumyrepositories/MusicStore.git',
                    branch: 'declarative'
            }
        }
        stage('build') {
            steps {
                sh 'dotnet build ./MusicStore/MusicSore.csproj'
            }
        }
        stage('test') {
            steps {
                sh 'dotnet test --logger "junit;LogFilePath=TEST-MusicStore.xml" ./MusicStore/MusicStore.csproj'
                junit testResult: '**/TEST-*.xml'
            }
        }
    }
    post {
        success {
            mail subject: "The ${JOB_NAME} job build id ${BUILD_ID} is success",
                 body: "See the more information about build using URL ${BUILD_URL}",
                 to: 'devops-team@decpl.in',
                 from: 'result@jenkins.job'
        }
    }
}