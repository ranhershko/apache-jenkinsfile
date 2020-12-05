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
      agent any
      steps {
        sh 'docker container run --name docker-apache-test -d "docker-apache:$BUILD_NUMBER"'
        sh 'curl http://$HOSTNAME'
      }
    }
  }
}
