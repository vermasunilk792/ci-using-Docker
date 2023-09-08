pipeline {
    agent any

          tools
    {
       maven "Maven"
    }
 stages {
      stage('checkout') {
           steps {

                git branch: 'master', url: 'https://github.com/vermasunilk792/ci-jenkins-docker.git'

          }
        }
         stage('Execute Maven') {
           steps {

                sh 'mvn package'
          }
        }
        //  stage('Docker user permission') {
        //    steps {

        //         sh 'docker run --rm -d --group-add $(stat -c '%g' /var/run/docker.sock) -v /var/run/docker.sock:/var/run/docker.sock -P samplewebapp:latest'

        //   }
        // }

         stage('Docker Build and Tag') {
           steps {

                sh 'docker build -t samplewebapp:latest .'
                //sh 'docker run --rm -d --group-add $(stat -c '%g' /var/run/docker.sock) -v /var/run/docker.sock:/var/run/docker.sock -P samplewebapp:latest'
                sh 'docker tag samplewebapp nikhilnidhi/samplewebapp:latest'
                
                //sh 'docker tag samplewebapp nikhilnidhi/samplewebapp:$BUILD_NUMBER'

          }
        }

        //  stage('Publish image to Docker Hub') {

        //     steps {
        //  withDockerRegistry([ credentialsId: "dockerHub", url: "" ]) {
        //   sh  'docker push nikhilnidhi/samplewebapp:latest'
        // //  sh  'docker push nikhilnidhi/samplewebapp:$BUILD_NUMBER'
        // }

        //   }
        // }

         stage('Run Docker container on Jenkins Agent') {

            steps
                        {
                sh "docker run -d -p 8003:8080 nikhilnidhi/samplewebapp"

            }
        }
         stage('Run Docker container on remote hosts') {

            steps {
                sh "docker -H ssh://ubuntu@54.92.145.81 run -d -p 8003:8080 nikhilnidhi/samplewebapp"

            }
        }
    }
        }

