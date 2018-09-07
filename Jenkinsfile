pipeline {
  agent {
    label 'java-maven'
  }
  stages {
    stage('Buzz Build') {
      steps {
        container('global-maven3-jdk8') {
          echo 'Keep Calm and Buzz'
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
              sh './jenkins/test-all.sh'
              junit '**/surefire-reports/**/*.xml'
            }
          }
        }
        stage('Testing B') {
          steps {
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
