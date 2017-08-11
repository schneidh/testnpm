pipeline {
    agent {
        docker 'node:7-onbuild'
    }
    stages {
      stage("a") {
        steps {
          withDockerContainer(args: "-u root", image: "node:7") {
            sh "npm install"
          }
        }
      }
    }
}
