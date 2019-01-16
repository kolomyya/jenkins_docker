node {
    def app

    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */

        checkout scm
    }
  

    stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */

        app = docker.build("u/kolomyya")
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
          docker.withRegistry('http://hub.docker.com/u/kolomyya') {
           app.push("${env.BUILD_NUMBER}")
           app.push("latest")
        }
    }
    stage('create container') {
           sh 'ssh -o StrictHostKeyChecking=no root@3.90.177.243 "sudo docker run -d  -p 8080:80 september:v4 " '
    }
}
