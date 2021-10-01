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

    stage('Example Stage 1') {
      steps {
        parallel(
            "step 1": { echo "hello" },
            "step 2": { echo "world" },
            "step 3": { echo "world" }
        )
      }
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