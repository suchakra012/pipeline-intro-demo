pipeline {
  agent any
  stages {
    stage('Buzz Build') {
      steps {
        echo 'Keep Calm and Buzz'
      }
    }
    stage('Buzz Test') {
      parallel {
        stage('Testing A') {
          steps {
            echo 'Testing A...'
          }
        }
        stage('Testing B') {
          steps {
            echo 'Testing B...'
	  }
        }
      }
    }
  }
  environment {
    BUZZ_NAME = 'Worker Bee'
  }
}
