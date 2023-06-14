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
        sleep 5
      }
    }

    stage('Test') {
      steps {
        sleep 5
      }
    }

    stage('Commit') {
      steps {
        sleep 5
      }
    }

  }
}