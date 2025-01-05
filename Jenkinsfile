pipeline {
agent any
tools {nodejs "npm"}
environment {
DOCKERHUB_CREDENTIALS= credentials(‘nargizzz’)
}
stages {
stage('Git Checkout') {

steps {
git branch: 'main', url: 'https://github.com/nargizrt/cicd-pipeline.git'
}
}
stage('Build App') {
steps {
sh '''chmod +x scripts/build.sh
./scripts/build.sh '''
}
}
stage('Test App') {
steps {
sh './scripts/test.sh'
}
}
stage('Build and Push the image to Docker Hub') {
steps {
script {
def nodeAppDockerfilePath = './Dockerfile'
sh "docker build -t nargizzz/n_cicd_image:$BUILD_NUMBER -f ${nodeAppDockerfilePath} ."
sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin
docker.io'
sh 'docker push nargizzz/n_cicd_image:$BUILD_NUMBER'
sh 'docker logout'
}
}
}
}
}