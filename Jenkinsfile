pipeline {
  agent none
  stages {
    stage('Buzz Build') {
      parallel {
        stage('Build Java 7') {
          agent {
            node {
              label 'java-maven'
            }
          }
          steps {
          container('global-maven3-jdk8') {
              echo 'Build Artifact Java 7'
              sh '''echo I am a $BUZZ_NAME
              ./jenkins/build.sh
              '''
              archiveArtifacts(artifacts: 'target/*.jar', fingerprint: true)
           }
          }
          post {
            always {
              echo 'Archive Artifact'
            }
            success {
              echo 'Stash Artifacts Java 7'
            }

          }
        }
        stage('Build Java 8') {
          agent {
            node {
              label 'java-maven'
            }

          }
          environment {
            BUZZ_NAME = 'Java 8 Bee'
          }
          steps {
 	          echo 'Build Artifact Java 8'
            echo 'Stash Artifacts Java 8'
          }
        }
      }
    }
    stage('Buzz Test') {
      parallel {
        stage('Testing A 7') {
          agent {
            node {
              label 'java-maven'
            }

          }
          steps {
            echo 'Buzz Java 7'
          }
        }
        stage('Testing B 7') {
          agent {
            node {
              label 'java-maven'
            }

          }
          steps {
            echo 'Buzz Java 7'
          }
        }
        stage('Testing A 8') {
          agent {
            node {
              label 'java-maven'
            }

          }
          steps {
            echo 'Buzz Java 8'
          }
        }
        stage('Testing B 8') {
          agent {
            node {
              label 'java-maven'
            }

          }
          steps {
            echo 'Buzz Java 8'
          }
        }
      }
    }
    stage('Confirm Deploy to Staging') {
      when {
        branch 'master'
      }
      steps {
        checkpoint 'Before Deploy'
        timeout(time: 3, unit: 'DAYS') {
          input(message: 'Deploy to Stage', ok: 'Yes, let\'s do it!')
        }

      }
    }
    stage('Deploy to Staging') {
      agent {
        node {
          label 'java-maven'
        }

      }
      when {
        branch 'master'
      }
      steps {
        echo "Deploying to ${DEPLOY_ENV}"
        echo 'Buzz Deploy Java 8'
      }
    }
  }
  environment {
    BUZZ_NAME = 'Worker Bee'
  }
  options {
    timeout(time: 5, unit: 'DAYS')
  }
  parameters {
    string(name: 'DEPLOY_ENV', defaultValue: 'staging', description: '')
  }
}
