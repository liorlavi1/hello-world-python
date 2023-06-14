pipeline {
  agent {
    node {
      label 'docker'
    }

  }
  stages {
    stage('checkout') {
      steps {
        git(url: 'https://github.com/liorlavi1/hello-world-python', branch: 'master')
      }
    }

    stage('Build') {
      steps {
        sh 'docker build -t liorlavi/hello-pipe:$BUILD_NUMBER .'
      }
    }

    stage('Test') {
      steps {
        sh 'docker run -itd --name testy 8000:8000 liorlavi/hello-pipe:$BUILD_NUMBER'
        sleep 5
        sh 'curl localhost:8000'
        sh 'docker stop testy && docker rm testy'
      }
    }

    stage('Push to dockerhub') {
      steps {
        sh 'docker login'
        sh 'docker push liorlavi/hello-pipe:$BUILD_NUMBER'
      }
    }

  }
}