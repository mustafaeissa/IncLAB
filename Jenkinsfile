pipeline {
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git 'https://github.com/mustafaeissa/Vtask'
      }
    }
    stage('Building & Pushing Imaages') {
      steps {
        withDockerRegistry(credentialsId: 'dockerhup', url: 'https://hub.docker.com') {
          sh 'ansible-playbook docker.yml'
        }
      }
    }
    stage('Test & Build CountriesApp') {
      steps {
        sh 'helm lint ./countries-app'
        sh 'helm install --name IncLAB ./countries-app'
      }
    }
    stage('Test & Build AirportsApp') {
      steps {
        sh 'helm lint ./airports-app'
        sh 'helm install --name IncLAB ./airports-app'
      }
    }
    stage('Install the ingress controller') {
      steps {
        sh 'helm install stable/nginx-ingress --name nginx-ingress --set controller.publishService.enabled=true'
      }
    }
    stage('Create ingress resource to expose Apps'){
      steps {
        sh 'kubectl apply -f ingress-nginx.yaml'
     }
   }
  }
}
