pipeline {
  agent any
  environment {
    GIT_REPOSITORY_URL = "https://github.com/bhavinprasad/docker_jenkins_demo.git"
    DOCKER_IMAGE_NAME = 'bhavinprasad/docker_jenkins_demo'
    IMAGE_TAG = '1.0'
  }
  stages {
    stage('Clone Repository') {
      steps {
        script {
          try {
            git branch: 'master', url: "https://github.com/bhavinprasad/docker_jenkins_demo.git"
          } catch (Exception e) {
            echo "failed to clone the repo ${e.message}"
            error "failed to clone"

          }
        }
      }
    }
    stage('Build Docker Image') {
      steps {
        script {
          try {
            docker.build("${DOCKER_IMAGE_NAME}:${IMAGE_TAG}")
          } catch (Exception e) {
            echo "failed to clone the repo ${e.message}"
            error "failed to clone"
          }
        }
      }
    }
    stage('Push To DockerHub') {
      steps {
        script {
          try {
            withCredentials([usernamePassword(credentialsId: '101', usernameVariable: 'bhavinprasad', passwordVariable: 'Password@1')]) {
              sh """
              docker login -u "bhavinprasad" -p "Password@1"
              docker push ${DOCKER_IMAGE_NAME}:${IMAGE_TAG}
              """
              
            }
          } catch (Exception e) {
            echo "failed to push the dockerimage ${e.message}"
            error "failed to push the Docker image"
          }
        }
      }
    }
  }
}
