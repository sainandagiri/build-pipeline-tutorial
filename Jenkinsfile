pipeline {
  agent any

  tools {
    jdk 'JDK 17'
  }

  stages {
    stage('Checkout') {
      steps {
        git 'https://github.com/sainandagiri/build-pipeline-tutorial.git'
      }
    }

    stage('Build App') {
      steps {
        sh './gradlew clean build'
      }
    }

    stage('Build Docker Image') {
      steps {
        sh 'docker build -t build-pipeline-demo .'
      }
    }

    stage('Run Docker Locally') {
      steps {
        sh 'docker run -d -p 8080:8080 build-pipeline-demo'
      }
    }
  }

  post {
    success {
      echo '✅ Build and Docker Image created successfully!'
    }
    failure {
      echo '❌ Build pipeline failed.'
    }
  }
}
