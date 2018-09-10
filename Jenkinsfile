pipeline {
  agent {
    label 'java-maven'
  }
  stages {
    stage('Buzz Build') {
      steps {
        container('global-maven3-jdk8') {
          echo 'Buzz Build'
          sh '''echo I am a $BUZZ_NAME
          ./jenkins/build.sh
          '''
          archiveArtifacts(artifacts: 'target/*.jar', fingerprint: true)
        }
      }
    }
    stage('Buzz Test') {
      parallel {
        stage('Testing A') {
          steps {
            container('global-maven3-jdk8') {
              echo 'Buzz Test A'
              sh './jenkins/test-all.sh'
              junit '**/surefire-reports/**/*.xml'
            }
          }
        }
        stage('Testing B') {
          steps {
            echo 'Buzz Test B'
            sh '''sleep 10
            echo done.'''
          }
        }
      }
    }
  }
  environment {
    BUZZ_NAME = 'Worker Bee'
  }
}
