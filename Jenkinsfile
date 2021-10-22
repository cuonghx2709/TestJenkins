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

    stage('Build') {
      steps {
        tool 'Gradle 7.2'
        tool 'JDK9'
        sh './gradlew assemble'
        archiveArtifacts '**/*.apk'
      }
    }

    stage('Security Testing using QARK') {
      when {
        expression {
          params.SecurityTesting == 'Yes'
        }

      }
      steps {
        sh '''source ~./bash_profile
qark --apk "app\\build\\outputs\\apk\\debug\\app-debug.apk"'''
      }
    }

  }
  parameters {
    choice(choices: ['Yes', 'No'], description: 'Do you want to perform Security Testing: ', name: 'SecurityTesting')
  }
}