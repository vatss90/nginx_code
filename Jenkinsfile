pipeline {
  agent {
    node {

    label 'slave'
}

}
  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub')
  }
  stages {
    stage('cloing') {
      steps {
        
        script {

            checkout scm  

      }
}    
}
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}
