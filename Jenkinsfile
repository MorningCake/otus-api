pipeline {
  agent any
  tools {
    jdk 'jdk11'
  }

  environment {
    MS_TEAMS_HOOK_URL = credentials('MSTeamsJenkinsHookURL')
    PITS_NEXUS = credentials('3bbdfcd0-c1be-411d-b330-30af8851df5d')
    DEVELOPMENT_VERSION = '1.0.0'
    PRODUCTION_VERSION = '1.0.0'
    QA_VERSION = '1.0.0'
  }

  stages {

    stage('Check environment') {
      steps{
        echo "The build number is ${BUILD_NUMBER}"
        echo "The branch is ${BRANCH_NAME}"
        sh 'java --version'
      }
    }

    stage('Build') {
      steps {
          sh '''
            ./gradlew clean build jar
          '''
      }
    }
  }

  post {
    always {
        office365ConnectorSend webhookUrl: "$MS_TEAMS_HOOK_URL"
    }
  }
}