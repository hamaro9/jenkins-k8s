pipeline {
  environment {
    dockerimagename = "docker-nexus-repo/react"
    dockerImage = ""
    KUBECONFIG = "/var/jenkins_home/.kube/config"
  }
  agent any
  stages {
    stage('Checkout Source') {
      steps {
        git branch: 'main', url: 'http://192.168.155.105:3005/slave/jenkins-kubernetes-deployment.git'
      }
    }
    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build dockerimagename
        }
      }
    }
    stage('Pushing Image') {
      environment {
        registryCredential = 'nexus-credentials'
      }
      steps{
        script {
          docker.withRegistry( 'http://192.168.155.105:5000', registryCredential ) {
            dockerImage.push("latest")
          }
        }
      }
    }
    stage('Deploying React.js container to Kubernetes') {
      steps {
        sh 'kubectl apply -f deployment.yaml'
        sh 'kubectl apply -f service.yaml'
      }
    }
  }
}
