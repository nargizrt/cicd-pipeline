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
       stage('Build a docker image') {
      steps {
        script {
          docker.build("${env.IMAGE_NAME}:${env.BUILD_NUMBER}")
        }

      }
    }
stage('Push') {
      steps {
        script {
          docker.withRegistry('https://registry.hub.docker.com', 'docker_hub_creds_id') {
            def app = docker.image("${env.IMAGE_NAME}:${env.BUILD_NUMBER}")
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")}
          }

        }
      }

    }
    environment {
      IMAGE_NAME = 'nargizrt/cicd-pipeline'
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