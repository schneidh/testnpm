pipeline {
    agent {
        docker 'node:7-onbuild'
    }
    stages {
      stage("a") {
        steps {
          withDockerContainer(args: "-u root", image: "${JOB_NAME}") {
            sh "npm install"
          }
        }
      }
    }
}
