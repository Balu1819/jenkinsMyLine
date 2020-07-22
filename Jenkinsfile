def FAILED_STAGE
pipeline {
  agent any
  stages {
    stage('Clone GIT1') {
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
        FAILED_STAGE=env.STAGE_NAME
        sh 'docker build .'
        post {
            failure {
            emailext body: "${FAILED_STAGE} stage got failed!!! Job_name: ${env.JOB_NAME} Build_number: ${env.BUILD_NUMBER}\n More info about the failure to Check console here to click: ${env.BUILD_URL}/console", recipientProviders: [[$class: 'DevelopersRecipientProvider']], subject: '$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS!', to: "${readProb['Recipent']}"
            }
            success {
               emailext body: " ${FAILED_STAGE} stage executed sucessfully,  Job_name:${env.JOB_NAME} Build_number: ${env.BUILD_NUMBER}\n More info about the job to Check console here to click: ${env.BUILD_URL}/console", recipientProviders: [[$class: 'DevelopersRecipientProvider']], subject: '$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS!', to: "${readProb['Recipent']}"
            }
        }
      }
    }

  }
}
