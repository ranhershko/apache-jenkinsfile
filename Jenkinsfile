pipeline {
  agent { node { label 'master' } }
  stages {
    stage('build dockerimage') {
      steps {
        script {
          dir('apache') {
            sh 'docker build -t "docker-apache:$BUILD_NUMBER" .'
          }
        }
      }
    }
    stage('docker container test') {
      steps {
        sh '''
          docker container run -d --name docker-apache-test "docker-apache:$BUILD_NUMBER"
          curl localhost
        '''
      }
    }
    stage('docker container deploy') {
      agent { node { label 'master' } }
      steps {
        sh '''
          docker tag "docker-apache:$BUILD_NUMBER" "docker-apache:latest"
          docker container restart -d --name docker-apache-prod "docker-apache:latest"
        '''
      }
    }
  }
  post {
    always {
      script {
        sh 'docker rm --force "docker-apache-test"'
      }
    }
  }
}
