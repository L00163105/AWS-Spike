pipeline {
  agent any
  tools {
    maven 'maven_3.6.1'
  }
  stages {
    stage('Build the application') {
      steps {
        echo "Build the application"
        sh 'mvn install'
      }
    }
    stage('Run tests') {
      steps {
        echo "Run tests"
      }
    }
    stage('deploy') {
      steps {
        echo "This is the deploy step"
      }
    }
  }
}