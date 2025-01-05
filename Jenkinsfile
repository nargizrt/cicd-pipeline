groovy
  pipeline {
      agent any
      stages {
          stage('Build') {
              steps {
                  script {
                      sh 'docker build -t n_cicd_image .'
                  }
              }
          }
          stage('Test') {
              steps {
                  script {
                      sh 'docker run n_cicd_image npm test'
                  }
              }
          }
          stage('Deploy') {
              steps {
                  script {
                      sh 'docker run -d n_cicd_image'
                  }
              }
          }
      }
  }