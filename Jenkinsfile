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
        sh 'docker run -itd --name testy -p 8080:8080 liorlavi/hello-pipe:$BUILD_NUMBER'
        sleep 10
        sh 'curl localhost:8080'
        sh 'docker stop testy && docker rm testy'
        cleanWs(cleanWhenFailure: true, cleanWhenAborted: true)
      }
    }

    stage('Push to dockerhub') {
      steps {
        withCredentials(bindings: [usernamePassword(credentialsId: 'docker-hub', passwordVariable: 'pass', usernameVariable: 'user')]) {
          sh "docker login -u $user -p $pass"
          sh "docker push liorlavi/hello-pipe:$BUILD_NUMBER"
        }

      }
    }

    stage('Clean Workspace') {
      steps {
        cleanWs(cleanWhenSuccess: true, cleanWhenFailure: true, cleanWhenAborted: true)
      }
    }

  }
}