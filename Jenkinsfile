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

    stage('Reporting') {
      steps {
        parallel(
            "Sonar Analysis": { echo "perform sonar analysis" },
            "Build/Push Docker Image": { echo "world" },
        )
      }
    }

    stage('Publish reports') {
      steps {
        publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: '/target/surefire-reports/com.ronan.githubactionsspike.GithubactionsspikeApplicationTests.txt', reportFiles: '', reportName: 'Test Report', reportTitles: ''])
      }
    }

    stage('Security Scan') {
      steps {
        echo "Deploying to test"
      }
    }

    stage('Deploy') {
    if (master) {
        steps {
          echo "Deploying to production"
        }
      }
    }
  }
}