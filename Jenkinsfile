def app
pipeline{ /* +develop branch */
  agent any

  stages{
    stage('SCM Checkout'){
      steps{
      git 'https://github.com/satyaelipe/front-end.git'
      }
    }

    stage('Build'){
      steps{
        script{
          app = docker.build("selipe/front-end")
          println "from Build"
        }
        }
    }


    stage('Test'){
      when {
                branch 'release'
            }
        steps {
          script{
           app.inside {
              println "Tests passed"
           }
          }

          }
    }

    stage('Push it to Docker Hub'){
      when {
              branch 'master'
          }
          steps{
           script{
           println "from push"
            /*def app = docker.build("selipe/node")*/
              docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials'){
              app.push("$env.BUILD_NUMBER")
              app.push("latest")
      }

      }
    }
  }
/*
  stage('Deploy to Minikube'){
    when {
            branch 'master'
        }
        steps{
         script{
         println "from Deploy"
            docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials'){
            app.push("$env.BUILD_NUMBER")
            app.push("latest")


    }

    }
  }
}
*/

}

}
