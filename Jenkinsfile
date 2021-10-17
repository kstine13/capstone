pipeline {
environment {
registry = "kstine13/capstone"
registryCredential = 'dockerhub_id'
dockerImage = ''
}
agent any
stages {
stage('Cloning our Git') {
steps {
git(
       url: 'https://github.com/kstine13/capstone.git',
       credentialsId: '0a806d1e-4c77-48e3-8528-b3daacb3a20d	',
       branch: "main"
    )
}
}
stage('Building our image') {
steps {
script {
dockerImage = docker.build registry + ":$BUILD_NUMBER"
}
}
}
stage ('Unit Tests') {
steps {
sh 'npm test'
}
}
stage('Deploy our image') {
steps {

script {
docker.withRegistry( '', registryCredential ) {
dockerImage.push()
}
}
}
}
stage('Cleaning up') {
steps {
sh "docker rmi $registry:$BUILD_NUMBER"
}
}
}
}
