node {
    def app

    stage('Clone repository') {
     
        checkout scm
    }
  

    stage('Build image') {
      
        app = docker.build("kolomyya/september")
    }

    stage('Test image') {
     
        app.inside {
            sh 'echo "Tests passed"'
        }
    }

   stage('Push image') {
    
         docker.withRegistry('https://registry.hub.docker.com', 'kolomyya') {
         app.push("${env.BUILD_NUMBER}")
          app.push("latest")
        }
    }
    
    stage('create container') {
           sh 'ssh -o StrictHostKeyChecking=no root@3.90.177.243 "sudo docker run -d  -p 8080:8000  kolomyya/september" '
    }
}
