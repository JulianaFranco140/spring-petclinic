#!groovy

pipeline {
  agent any 

  tools {
    maven 'Maven 3' 
  }

  stages {
    stage('Maven Install') {
      steps {
        sh 'mvn clean package -DskipTests' 
      }
    }
    
    stage('Docker Build') {
      steps {
        sh 'docker build -t docker.io/JulianaFranco140/spring-petclinic:gestion-udem-jenkins .'
      }
    }
    
    stage('Docker Push') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
          sh "echo \"${env.dockerHubPassword}\" | docker login -u \"${env.dockerHubUser}\" --password-stdin docker.io"
          
          sh 'docker push docker.io/julianafranco140/spring-petclinic:gestion-udem-jenkins'
        }
      }
    }
  }
}