pipeline {
   agent any
   stages {
       stage('Preparation') {
           steps {
               // Check out the source code from your repository
               checkout scm
           }
       }
       stage('Set Permissions') {
           steps {
               // Make the build script executable
               sh 'chmod +x scripts/build.sh'
           }
       }
       stage('Build') {
           steps {
               // Run the build script
               sh './scripts/build.sh'
           }
       }
       stage('Test') {
           steps {
               // Run the test script
               sh './scripts/test.sh'
           }
       }
       stage('Build Docker Image') {
           steps {
               // Build the Docker image
               sh 'docker build -t n_cicd_image .'
           }
       }
   }
   post {
       success {
           echo 'Pipeline completed successfully!'
       }
       failure {
           echo 'Pipeline failed. Please check the logs.'
       }
   }
}