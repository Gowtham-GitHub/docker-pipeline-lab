pipeline {
    agent { label 'Java' }
    stages { 
        stage ("SCM Checkin-1") {
            steps {
              git branch: 'master', url: 'https://github.com/Gowtham-GitHub/MavenRepo'
            }
        }
        stage ("maven build") {
            tools {
                maven 'Maven v3.8.2'
                jdk 'JDK1.8'
            }
            steps {
                sh "mvn package"
            }
        input {
                 message 'Mvn Package is Successfull, I can Proceed'
            }
        }
        stage ("Build the Docker Image") {
            steps {
                sh "sudo docker build . -t gowtham994433/tomcat-b15"
            }
        }
        stage ("Run the Container") {
            steps {
                sh "sudo docker run -d -p 90:8080 --name cont01 gowtham994433/tomcat-b15"
            }
        }
      //  stage ("Check the webpage") {
      //      steps {
      //          sh "sleep 15"
      //          sh "curl http://192.168.118.105:90/mvn-hello-world"
      //      }
      //  }
        stage ("Push to Docker HUB") {
            steps {
        // some block
            sh "sudo docker push gowtham994433/tomcat-b15:latest"
            }
        }
        stage ("Cleanup the previous Docker Image and container") {
            input {
                    message 'Can we Delete the Docker image and Container'
            }
            steps {
                sh "sudo docker rm cont01 -f"
                sh "sudo docker image rmi gowtham994433/tomcat-b15 -f"
        //sh "mvn clean"
            }
        }
    }
}
