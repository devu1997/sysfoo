pipeline {
  agent none
  stages {
    stage('build') {
      agent {
        docker {
          image 'maven:3.8.5-jdk-11-slim'
        }

      }
      steps {
        echo 'Compiling...'
        sh 'mvn compile'
      }
    }

    stage('test') {
      agent {
        docker {
          image 'maven:3.8.5-jdk-11-slim'
        }

      }
      steps {
        echo 'Running unit tests...'
        sh 'mvn clean test'
      }
    }

    stage('package') {
      agent {
        docker {
          image 'maven:3.8.5-jdk-11-slim'
        }

      }
      steps {
        echo 'Generating artifact...'
        sh 'mvn package -DskipTests'
        archiveArtifacts 'target/*.war'
      }
    }

    stage('docker-build-publish') {
      agent any
      steps {
        script {
          docker.withRegistry('https://index.docker.io/v1/', 'dockerlogin') {
            def dockerImage = docker.build("dev1997/sysfoo:v${env.BUILD_ID}", "./")
            dockerImage.push()
            dockerImage.push("latest")
            dockerImage.push("dev")
          }
        }

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