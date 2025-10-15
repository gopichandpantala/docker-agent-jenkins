pipeline {
  agent {
    docker {
      image 'maven:3.9.6-eclipse-temurin-17'
      args '-v /root/.m2:/root/.m2'
    }
  }

  stages {
    stage('Checkout') {
      steps {
        echo 'Checking out source code...'
        checkout scm
      }
    }

    stage('Build') {
      steps {
        echo 'Building the project...'
        sh 'mvn clean package -DskipTests'
      }
    }

    stage('Test') {
      steps {
        echo 'Running tests...'
        sh 'mvn test'
      }
    }
  }

  post {
    success {
      echo '✅ Build and tests completed successfully!'
    }
    failure {
      echo '❌ Build or test failed.'
    }
  }
}
