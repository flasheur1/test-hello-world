node{
  stage ('SCM Checkout') {
    tool name:'maven-3', type: 'maven'
    git url: 'https://github.com/flasheur1/test-hello-world'
  }
  
  stage ('Compile-Package') {
    sh 'mvn clean install'
  }
}
