pipeline {
  agent none 
  triggers {
      pollSCM('* * * * *')
  }   
  stages { 
    stage('Run tests') {
      environment {
        HOME = '.'
      }
        agent {
          docker {
            image 'node:8-alpine'
            args '-p 3000:3000'
          }
        }
      
        stages {
          stage('Build') {
            environment {
              HOME = '.'
            }
            steps {
              sh 'npm install'
            }
          }
          stage('Test') {
            environment {
              HOME = '.'
            }
            steps {
              sh 'npm test'
            }
          }
        }
      }

      stage('Deploy app to development') {
        environment {
          HOME = '.'
        }
          when {
              branch 'Development'
          }
          agent any 
          steps {
              sh 'echo hello'
          }
      }

    stage('Deploy app to production') {
      environment {
        HOME = '.'
      }
        when {
            branch 'master'
        }
        agent any 
        steps {
              sh 'echo hello'
        }
    }
  }
}
