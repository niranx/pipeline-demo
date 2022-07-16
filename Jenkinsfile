pipeline{
  environment {
    REPO = 'niranx/demo-pipeline'
  }

  agent any
  
  stages {
    stage('Docker Build'){
      steps {
        sh "docker build -t $REPO:v$BUILD_NUMBER ."
      }
    }
    stage('Docker Push') {
      steps {
        withCredentials([usernamePassword(
          credentialsId: 'dockerhub-access',
          usernameVariable: 'User',
          usernamePassword: 'Password'
        )]) {
          sh "docker login -u ${env.User} -p ${env.Password}"
          sh "docker push $REPO:v$BUILD_NUMBER"
        }
      }
    }
    stage('House Keeping'){
      steps {
        sh "docker rmi $REPO:v$BUILD_NUMBER"
      }
    }
  }
}