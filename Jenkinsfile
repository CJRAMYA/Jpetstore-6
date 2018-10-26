pipeline {
  agent any
  stages {
    stage('Recuperation des sources') {
      steps {
        git(url: 'https://github.com/CJRAMYA/Jpetstore-6.git', branch: 'master', credentialsId: '4abfae6d-c653-4cb3-8841-46a36185915b')
      }
    }
    stage('build maven') {
      steps {
        bat(encoding: 'utf-8', script: 'runmaven.bat')
      }
    }
  }
}