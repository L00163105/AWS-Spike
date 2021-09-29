pipeline {

  def buildNumber = env.BUILD_ID
  def buildUrl = env.JENKINS_URL

  agent any
  tools {
    maven 'maven_3.6.1'
  }
  stages {
    stage('Build the application') {
      steps {
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
        echo "This is the deploy step " + buildUrl
        echo "This is the deploy step " + buildNumber
        echo "This is the deploy step " + BRANCH_NAME
      }
    }
  }
}