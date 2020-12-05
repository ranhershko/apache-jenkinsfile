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
        sh 'docker container run -p 8"$BUILD_NUMBER":80 -d "docker-apache:$BUILD_NUMBER"'
        sh "grep -i bluesnap /var/www/html/index.html"
      }
    }
  }
}
