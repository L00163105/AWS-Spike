pipeline {
  agent any
  tools {
    maven 'apache-maven'
  }
  stages {
    stage('build') {
      steps {
        echo "This is my buid step"
        sh 'mvn --version'
      }
    }
    stage('package') {
      steps {
        echo "This is the package step"
      }
    }
    stage('deploy') {
      steps {
        echo "This is the deploy step"
      }
    }
  }
}