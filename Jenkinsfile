pipeline {
  agent {
    docker {
      image 'maven:3.8.5-jdk-11-slim'
    }

  }
  stages {
    stage('build') {
      steps {
        echo 'Compiling...'
        sh 'mvn compile'
      }
    }

    stage('test') {
      steps {
        echo 'Running unit tests...'
        sh 'mvn clean test'
      }
    }

    stage('package') {
      steps {
        echo 'Generating artifact...'
        sh 'mvn package -DskipTests'
        archiveArtifacts 'target/*.war'
      }
    }

  }
  tools {
    maven 'Maven 3.8.5'
  }
  post {
    always {
      echo 'this pipeline has completed...'
    }

  }
}