def buildNumber = env.BUILD_ID
def buildUrl = env.JENKINS_URL

pipeline {

  agent any
  tools {
    maven 'maven_3.6.1'
  }
  stages {
    stage('Build the application') {
      steps {
        sh 'mvn clean install -DskipTests'
      }
    }
    stage('Run tests') {
      steps {
        sh 'mvn test'
      }
    }

    stage('Run adfg') {
      parallel firstBranch: {
        echo "This is the deploy step"
      }, secondBranch: {
        echo "This is the deploy step "
      },
          failFast: true|false
    }

    stage('deploy') {
      steps {
        echo "This is the deploy step " + buildUrl
        echo "This is the deploy step " + buildNumber
        echo "This is the deploy step " + env.BRANCH_NAME
      }
    }
  }
}