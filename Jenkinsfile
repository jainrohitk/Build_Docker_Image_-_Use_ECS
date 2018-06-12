pipeline {
  agent any

  // Set any variables here
  environment {
    IMAGE_NAME = 'jainrohitk/node'
    DOCKER_FILE = 'Dockerfile'
  }

  stages {

    // Build the test container  and save it
    stage('Build test container') {
      steps {
        script {
          def testImage = docker.build($IMAGE_NAME, "-f ${$DOCKER_FILE} .")
        }
      }
    }
  }
}
