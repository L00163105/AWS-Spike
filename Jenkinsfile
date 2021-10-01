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
        sh 'mvn clean install'
      }
    }

    stage('Reporting') {
      steps {
        parallel(
            "Sonar Analysis": { echo "perform sonar analysis" },
            "Build/Deploy Docker Image": { echo "world" },
        )
      }
    }

    stage('Deploy to test') {
      steps {
        echo "Deploying to test"
      }
    }

    stage('deploy') {
      steps {
        echo "Deploying to production " + buildUrl
      }
    }
  }
}