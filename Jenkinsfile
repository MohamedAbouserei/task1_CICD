
pipeline {
environment {
registry = "mohamedabouserei/task1_cicd"
registryCredential = 'dockerhub_id'
dockerImage = ''
}
agent any
stages {
stage('Cloning our Git') {
steps {
git 'https://github.com/MohamedAbouserei/task1_CICD.git'
}
}
stage('build') {
      steps {
        sh 'pip install -r requirements.txt'
      }
    }
    stage('test') {
      steps {
        sh 'python tests/test.py'
      }   
    }
stage('Building our image') {
steps{
script {
dockerImage = docker.build registry + ":$BUILD_NUMBER"
}
}
}
stage('Deploy our image') {
steps{
script {
docker.withRegistry( '', registryCredential ) {
dockerImage.push()
}
}
}
}
stage('Cleaning up') {
steps{
sh "docker rmi $registry:$BUILD_NUMBER"
}
}
stage('Ec2 Deploy') {
steps{
sh "ssh ec2-user@ec2-18-191-146-246.us-east-2.compute.amazonaws.com"  
sh "docker pull $registry:$BUILD_NUMBER"
sh "docker container run --name jenkins2 -d -p 8080:8080 $registry:$BUILD_NUMBER"

}
}
}
}
