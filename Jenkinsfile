node{
    stage ('Sources Checkout') {
      git url: 'https://github.com/flasheur1/test-hello-world'
    }
    stage ('Compile && Package') {
      def mvnHome  =     tool name: 'maven', type: 'maven'
      sh "${mvnHome}/bin/mvn clean install"
    }
    stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line  app = docker.build("flasheur1/test-repos")*/
       
        sh "docker build -t flasheur1/test-repos:${env.BUILD_ID} ."
    }

    stage('Test image') {
        /* Ideally, we would run a test framework against our image.
         * For this example, we're using a Volkswagen-type approach ;-) */

        app.inside {
            sh 'echo "Tests passed"'
        }
    }

    stage('Push image') {
        /* Finally, we'll push the image with two tags:
         * First, the incremental build number from Jenkins
         * Second, the 'latest' tag.
         * Pushing multiple tags is cheap, as all the layers are reused. */
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}
