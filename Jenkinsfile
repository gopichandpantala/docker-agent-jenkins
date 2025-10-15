pipeline {
  agent {
    docker {
      image 'maven:3.9.6-eclipse-temurin-17'
      args '-v /root/.m2:/root/.m2 -v /var/run/docker.sock:/var/run/docker.sock'
    }
  }

  stages {
    stage('Checkout') {
      steps { checkout scm }
    }

    stage('Build') {
      steps {
        sh 'mvn clean package -DskipTests'
      }
    }

    stage('Test') {
      steps { sh 'mvn test' }
    }
  }

  post {
    always {
      echo '🧹 Cleaning up containers and images on host...'
      sh '''
        docker container prune -f || true
        docker image prune -af || true
        docker network prune -f || true
        docker volume prune -f || true
      '''
    }
  }
}
