def main = env.BRANCH_NAME == "master"
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

    stage('Security Scan') {
      steps {
        echo "Performing Security Scan"
      }
    }

    stage('Deploy') {
      steps {
        script {
          if (main) {
            echo 'Deploy to production'
          } else {
            echo 'Deploy to test'
          }
        }
      }
    }

    stage('Email') {
      steps {
        parallel(
            "Email L00163105": { echo "emailing team" },
            "Email deploys": { echo "emailing deploys" },
        )
      }
    }
  }
}