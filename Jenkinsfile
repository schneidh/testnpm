pipeline {
    agent {
        docker 'node:7-onbuild'
    }
    stages {
      withDockerContainer(args: "-u root", image: "${JOB_NAME}") {
        stage("check node") {
            sh "npm install"
        }
      }
    }
}
