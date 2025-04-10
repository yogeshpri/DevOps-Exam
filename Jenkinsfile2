pipeline {
  agent any
  environment {
      DOCKER_IMAGE = 'devopstest:latest'
      CONTAINER_NAME = 'java-web-app-cicd'
      DOCKER_USERNAME = 'yogeshpri'
      DOCKER_PASSWORD = 'dckr_pat_cs1MmwA_v_FPnEJxWgj0'
      DOCKER_REPO = 'yogeshpri/devopstest:latest'
  }
  stages {
      stage('Clone Repository') {
          steps {
              script {
                  // Dynamically clone the branch based on the manually set branch name
                  git branch: "main", url: 'https://github.com/yogeshpri/DevOps-Exam'
              }
          }
      }
      stage('Build Image & Push to Docker Hub') {
          steps {
              script {
                  // Build Docker image
                  sh "docker build -t ${DOCKER_REPO} ."
                  echo "Docker image build successfully completed."
                  // Login to Docker Hub
                  sh "echo ${DOCKER_PASSWORD} | docker login -u ${DOCKER_USERNAME} --password-stdin"
                  // Push Docker image
                  sh "docker push ${DOCKER_REPO}"
              }
          }
      }
      stage('Create Deployment') {
          steps {
              script {
                  // Apply deployment.yaml
                  sh 'kubectl apply -f deployment.yaml'
                      sh 'kubectl apply -f services.yaml'
                  }
              }
          }
      }
  }

