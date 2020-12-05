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
        sh 'docker container run -p 81:80 -d "docker-apache:$BUILD_NUMBER"'
        sh 'curl http://localhost:81'
      }
    }
  }
}
