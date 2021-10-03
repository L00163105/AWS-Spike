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
            "Build/Push Docker Image": { echo "world" },
        )
      }
    }

    stage('Publish reports') {
      steps {
        publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: '/target/surefire-reports/com.ronan.githubactionsspike.GithubactionsspikeApplicationTests.txt', reportFiles: '', reportName: 'Test Report', reportTitles: '']),
        junit()
      }
    }

    stage('Security Scan') {
      steps {
        echo "Deploying to test"
      }
    }

//    var master = env.BRANCH_NAME == "master"
//
    stage('Deploy') {
      steps {
//        if(master) {
        echo "Deploying to production"
//        } else {
//          echo "Deploying to test"
//        }
      }
    }
  }
}