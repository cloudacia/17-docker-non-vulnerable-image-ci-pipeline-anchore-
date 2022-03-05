pipeline {
  agent any
    environment {
        registry = "eduarte/linux-tweet-app"
        registryCredential = 'dockerhub_id'
        dockerImage = ''
      }

    stages {
      stage('Cloning our Git') {
        steps {
          git 'https://github.com/cloudacia/linux_tweet_app.git'
        }
      }

      stage('Building our image') {
        steps {
          sh "docker build -t $registry:$BUILD_NUMBER ."

        }
      }

      stage('usernamePassword') {
      steps {
        script {
          withCredentials([
            usernamePassword(credentialsId: "$registryCredential",
              usernameVariable: 'username',
              passwordVariable: 'password')
          ]) {
            sh "docker login -u $username -p $password"
            sh "docker push $registry:$BUILD_NUMBER"

          }
        }
      }
    }

      //stage('Deploy our image') {
      //  steps {
      //    script
            //sh "docker login -u eduarte -p eugenio23"
            //sh "docker push $registry:$BUILD_NUMBER"
    //      }
    //    }
    //  }

      stage('Cleaning up') {
        steps {
          sh "docker rmi $registry:$BUILD_NUMBER"
        }
      }
    }
  }
