pipeline {
  agent any
  tools {
    maven 'maven_3.6.1'
  }
  stages {
    stage('Build the application') {
      steps {
        echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
        sh 'mvn install'
      }
    }
    stage('Run tests') {
      steps {
        sh 'mvn test'
      }
    }
    stage('deploy') {
      steps {
        echo "This is the deploy step"
      }
    }
  }
}