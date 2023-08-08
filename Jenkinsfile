pipeline {
   enviroment {
     REPO_NAME="vatss90/nginx_new"

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

stage ('image creation') {
     
                steps {
				sh 'docker build -t ${REPO_NAME}:${env.GIT_COMMIT[0..6]} .'
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
