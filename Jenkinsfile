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
            sh '''cd /home/magento/Documents/Docker/omc-2.0/app/code/Magestore
git clone https://magestore-system:bcdf5baeee5c56a052cecb90ff7a0295f188d750@github.com/Magestore/webpos-omc-2.0 -b develop Webpos
echo \'clone successfully.\''''
          }
        }
        stage('Client') {
          agent {
            docker {
              image 'node:9'
            }
            
          }
          steps {
            sh '''cd /home/magento/Documents/Docker/omc-2.0/app/web
git clone https://magestore-system:bcdf5baeee5c56a052cecb90ff7a0295f188d750@github.com/Magestore/webpos-client-omc-2.0 -b develop webpos-client-omc-2.0
echo \'clone client successfully.\''''
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