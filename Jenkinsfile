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
        bat '''
          docker stop build-pipeline-demo || exit 0
          docker rm build-pipeline-demo || exit 0
          docker run -d -p 9090:8080 --name build-pipeline-demo build-pipeline-demo
        '''
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
