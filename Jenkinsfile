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
        sh "docker build -t  $REPO_NAME:${GIT_COMMIT[0..6]} ."
  }
      }      
}
stage('push') {
      steps {
       sh "docker push $REPO_NAME:${GIT_COMMIT[0..6]}"

      }
}

stage('Pass image to cdbuild'){
  steps{
     script{
       build job: 'nginx_cd_1',
       parameters: [string(name:'IMAGE_TAG', value:"${GIT_COMMIT[0..6]}")]
       parameters: [string(name:'REPOSITORY_NAME', value:"$REPO_NAME")]

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
