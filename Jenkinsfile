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

    emailext (to: 'abc@gmail.com', replyTo: 'ronan.clancy@gmail.com', subject: "Email Report from - '${env.JOB_NAME}' ", body: readFile("target/surefire-reports/com.ronan.githubactionsspike.GithubactionsspikeApplicationTests.txt"), mimeType: 'text/html');
  }
}