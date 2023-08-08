pipeline {

  agent {
    node {

    label 'slave'
}

}
  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub')
    REPO_NAME = "vatss90/nginx_new"
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

   stage('bulid') {
      steps {
 script { 
        sh 'docker build -t  vatss90/nginx:v1 .'
  }
      }      
}

}
  post {
    always {
      sh 'docker logout'
    }
  }
}
