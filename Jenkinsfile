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
            environment {
                
                DOCKER_CREDS = credentials('docker-hub-credentials')
            }
            steps {
                sh '''              
                echo "$DOCKER_CREDS_PSW" | docker login -u "$DOCKER_CREDS_USR" --password-stdin
                
                docker push lexxkz/mybuildimage
                '''
            }
        }
    }
}
