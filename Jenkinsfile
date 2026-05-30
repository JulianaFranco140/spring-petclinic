#!groovy

pipeline {

  agent any 

  stages {
    stage('Maven Install') {
      steps {
        sh 'mvn clean package -DskipTests' 
      }
    }
    
    stage('Docker Build') {
      steps {
        sh 'docker build -t JulianaFranco140/spring-petclinic:gestion-udem-jenkins .'
      }
    }
    
    stage('Docker Push') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
          sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
          sh 'docker push JulianaFranco140/spring-petclinic:gestion-udem-jenkins'
        }
      }
    }
  }
}