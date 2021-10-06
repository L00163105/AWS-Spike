def main = env.BRANCH_NAME == "master"
pipeline {

  /**
   * set agent to any if no agents are configured
   */
  agent any

  /**
   * tool
   */
  tools {
    maven 'maven_3.6.1'
  }

  /**
   * Optional: options we can set for our script
   */
  options {
    parallelsAlwaysFailFast() // Fail the job and don't continue to the next step if parallel step fails
  }

  /**
   * Stages block, defines all stages of our pipeline
   */
  stages {

    stage('Build the application') {
      steps {
        sh 'mvn clean install'
      }
    }

    /**
     * Sonar and Docker: Here we have setup a parallel block to analise
     * and push our docker image.
     */
    stage('Sonar and Docker') {
      steps {
        parallel(
            "Sonar Analysis": { echo "perform sonar analysis" },
            "Build/Push Docker Image": { echo "building and pushing docker image-" + env.BUILD_ID }
        )
      }
    }

    stage('Security Scan') {
      steps {
        echo "Performing Security Scan"
      }
    }

    /**
     * Deploy Block: Here we have setup out conditional block
     * using the var set on line 1
     */
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

    /**
     * Notifications: Here we have setup a parallel block to send
     * notifications
     */
    stage('Notifications') {
      steps {
        parallel(
            "Email L00163105": { echo "emailing team" },
            "Slack Channel Notification": { echo "emailing deploys" },
        )
      }
    }

    /**
     * post: This block will always be always executed even if steps fails
     * of succeed above.
     */
    post {
      always {
        echo 'Clean up cache'
      }
    }
  }
}