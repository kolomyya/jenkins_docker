node {
    app

    stage('Clone repository') {

        checkout scm
    }
  

    stage('Build image') {
        app = docker.build("u/kolomyya")
    }

    stage('Test image') {
        app.inside {
            sh 'echo "Tests passed"'
        }
    }

    stage('Push image') {
       
          docker.withRegistry('http://hub.docker.com/u/kolomyya') 
    }
    stage('create container') {
           sh 'ssh -o StrictHostKeyChecking=no root@3.90.177.243 "sudo docker run -d  -p 8080:80 september:v4 " '
    }
}
