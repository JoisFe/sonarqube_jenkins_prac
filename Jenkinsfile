pipeline {
  agent any
  stages {
    stage('체크아웃') {
      steps {
        checkout scm
      }
    }

    stage('소나큐브 스캔') {
      steps {
        script {
          withSonarQubeEnv('test') {
            sh './gradlew sonar -Dsonar.source=src'
          }
        }
      }
    }
  }
  post {
    always {
      script {
        if (waitForQualityGate().status != 'OK') {
          echo "소나큐브 스캔 실패"
          currentBuild.result = '실패'
        }
      }
    }
  }
}