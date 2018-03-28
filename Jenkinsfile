pipeline {
  agent any
  stages {
    stage('Build Product') {
      parallel {
        stage('Server') {
          agent {
            docker {
              image 'maven:3.5-jdk-8-slim'
            }
            
          }
          steps {
            sh '/home/magento/Documents/Jenkins/ContinuousIntergration/server.sh'
          }
        }
        stage('Client') {
          agent {
            docker {
              image 'node:9'
            }
            
          }
          steps {
            sh '/home/magento/Documents/Jenkins/ContinuousIntergration/client.sh'
          }
        }
      }
    }
    stage('Automation Test') {
      parallel {
        stage('Chrome') {
          agent {
            docker {
              image 'selenium/standalone-chrome'
            }
            
          }
          steps {
            sh 'echo \'mvn test -Dbrowser=chorme\''
          }
        }
        stage('Firefox') {
          agent {
            docker {
              image 'selenium/standalone-firefox'
            }
            
          }
          steps {
            sh 'echo \'mvn test -Dbrowser=firefox\''
          }
        }
      }
    }
    stage('Build Test Log') {
      parallel {
        stage('Write Log') {
          agent any
          steps {
            sh 'echo \'abc\''
          }
        }
        stage('Slack Message') {
          steps {
            sh 'Slack Messages'
          }
        }
      }
    }
    stage('Done') {
      agent any
      steps {
        echo 'c'
      }
    }
  }
}