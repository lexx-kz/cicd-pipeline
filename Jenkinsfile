pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'script scripts/build.sh'
      }
    }

    stage('Test') {
      steps {
        sh '''script scripts/test.sh
'''
      }
    }

    stage('Docker Build') {
      steps {
        sh 'docker build -t lexxkz/mybuildimage .'
      }
    }

    stage('Docker Push') {
      steps {
        sh '''docker.withRegistry(\'https://registry.hub.docker.com\', \'docker-hub-credentials\') {
    // This tells Jenkins to use the \'mybuildimage\' we built earlier
    // and push it to Docker Hub using the credentials provided
    docker.image(\'lexxkz/mybuildimage\').push(\'latest\')
}
'''
        }
      }

    }
  }