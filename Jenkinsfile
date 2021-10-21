pipeline {
  agent any
  stages {
    stage('Lint Analysis') {
      steps {
        tool 'Gradle 7.2'
        sh './gradlew lint'
      }
    }

    stage('Unit Test') {
      steps {
        tool 'Gradle 7.2'
        tool 'JDK9'
        sh 'gradle jacocoTestReportDebug '
        junit '**/testDebugUnitTest/*.xml'
      }
    }

  }
}