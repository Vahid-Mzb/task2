pipeline {
  agent any
  environment {
    DOCKER_IMAGE = 'mynodeapp:${BUILD_NUMBER}'
  }
  stages {
    stage('Build') {
      steps {
        script {
          docker.build(env.DOCKER_IMAGE)
        }
      }
    }
    stage('Test') {
      steps {
        script {
          // Assume tests are defined
          sh 'npm test'
        }
      }
    }
    stage('Deploy') {
      steps {
        script {
          // Use Kubernetes plugin to deploy
          kubernetesDeploy(kubeconfigId: 'minikube', configs: 'k8s/*.yaml')
        }
      }
    }
  }
}
