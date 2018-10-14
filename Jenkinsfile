node{
    
  environment {
    registry = "flasheur1/test-repos"
    registryCredential = 'docker-hub-credentials'
    dockerImage = ''
  }
    stage ('Sources Checkout') {
      git url: 'https://github.com/flasheur1/test-hello-world'
    }
    stage ('Compile && Package') {
      def mvnHome  =     tool name: 'maven', type: 'maven'
      sh "${mvnHome}/bin/mvn clean install"
    }

    stage('Building Image') {
      dockerImage = docker.build registry + ":$BUILD_NUMBER"
    }

    stage('Deploy Image') {
      docker.withRegistry('',registryCredential) {
        dockerImage.push()
      }
    }
}
