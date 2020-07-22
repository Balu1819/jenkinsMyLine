pipeline {
  agent any
  stages {
    stage('Clone GIT') {
      steps {
        git(url: 'https://github.com/Balu1819/hello-world.git', credentialsId: 'balu1819', branch: 'master')
      }
    }

    stage('build') {
      steps {
        sh 'mvn clean package'
      }
    }

    stage('buld image') {
      steps {
        sh 'docker build .'
      }
    }

  }
}