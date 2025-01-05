pipeline {
   agent any
tools {nodejs "nodes"}
   stages {
       stage('checkout') {
           steps {
git branch: 'main', url: 'https://github.com/nargizrt/cicd-pipeline.git'
}
       }
       stage('build app') {
           steps {
               sh 'chmod +x scripts/build.sh'
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