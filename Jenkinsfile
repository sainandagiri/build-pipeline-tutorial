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
        bat '.\\gradlew.bat clean build'
      }
    }

    stage('Build Docker Image') {
      steps {
        bat 'docker build -t build-pipeline-demo .'
      }
    }

    stage('Run Docker') {
      steps {
        bat 'docker run -d -p 8080:8080 build-pipeline-demo'
      }
    }
  }

  post {
    success {
      echo '✅ Build completed!'
    }
    failure {
      echo '❌ Something went wrong.'
    }
  }
}
