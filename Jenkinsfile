#!groovy

pipeline {
  agent none
  stages {
    stage('Maven Install') {
      agent {
        docker {
          image 'maven:3.9-eclipse-temurin-25' 
          reuseNode true
        }
      }
      steps {
        sh 'mvn clean' 
      }
    }
    stage('Docker Build'){
      agent any
      steps {
        sh 'docker build -t JulianaFranco140/spring-petclinic:gestion-udem-jenkins .'
      }
    }
    stage('Docker Push') {
      agent any
      steps {
        withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
          sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
          sh 'docker push <docker-username>/spring-petclinic:gestion-udem-jenkins'
        }
      }
    }
  }
}
