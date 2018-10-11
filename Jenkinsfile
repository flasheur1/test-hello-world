node{
  stages {
    stage ('Sources Checkout') {
      git url: 'https://github.com/flasheur1/test-hello-world'
    }

    stage ('Compile && Package') {
      def mvnHome  =     tool name: 'maven', type: 'maven'
      sh "${mvnHome}/bin/mvn clean install"
    }
  }
}
