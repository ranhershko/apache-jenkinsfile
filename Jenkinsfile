pipeline {
  agent none
  stages {
    stage('build dockerimage') {
      agent any
      steps {
        script {
          dir('apache') {
            def image = docker.build("docker-apache:$BUILD_NUMBER")
          }
        }
      }
    }
    stage('Test dockerimage container') {
      agent {
        docker { image "docker-apache:$BUILD_NUMBER" }
      }
      steps {
        sh 'curl http://localhost'
      }
    }
  }
}
