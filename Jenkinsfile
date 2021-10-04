def master = env.BRANCH_NAME == "master"
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

    stage('Sonar and Docker') {
      steps {
        parallel(
            "Sonar Analysis": { echo "perform sonar analysis" },
            "Build/Push Docker Image": { echo "building and pushing docker image" },
        )
      }
    }

    stage('Publish reports') {
      steps {
        echo 'Emailing Test Reports'
      }
    }

    stage('Security Scan') {
      steps {
        echo "Performing Security Scan"
      }
    }

    stage('Deploy') {
      steps {
        script {
          echo env.BRANCH_NAME
          if (master) {
            echo 'Deploy to production'
          } else {
            echo 'Deploy to test'
          }
        }
      }
    }
  }
}