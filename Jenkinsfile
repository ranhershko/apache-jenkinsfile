pipeline {
  agent none
  stages {
    stage('build dockerimage') {
      agent any
      steps {
        script {
          dir('apache') {
            sh 'docker build -t "docker-apache:$BUILD_NUMBER" .'
          }
        }
      }
    }
    stage('Test dockerimage container') {
      agent { node { label 'master' } }
      steps {
        sh 'docker container run --restart=always -d "docker-apache:$BUILD_NUMBER"; curl localhost'
      }
    }
  }
}
