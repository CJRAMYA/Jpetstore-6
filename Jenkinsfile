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
	stage('qualimetrie') {
      steps {
        withSonarQubeEnv('SonarQube') {
			bat(script: 'runqualimetrie.bat', encoding: 'UTF-8')   
		}
      }
    }
	stage('quality gate') {
      steps {
		sleep 10
        timeout(time:3, unit:'MINUTES'){
			waitForQualityGate abortPipeline: true
		}
      }
    }
	 stage('Publication') {
      steps {
        nexusArtifactUploader(
		nexusVersion: 'nexus3', 
		protocol: 'http', 
		nexusUrl: 'localhost:8081', 
		groupId: 'org.mybatis', 
		version: '0.0.1-SNAPSHOT', 
		repository: 'maven-snapshots', 
		credentialsId: 'bdf8ef1a-2969-48a6-9e45-a265ae641a8a', 
		artifacts: [[
		artifactId: 'jpetstore', 
		type: 'war', 
		file: 'target/jpetstore-0.0.1-SNAPSHOT.war']])
      }
    }
  }
}