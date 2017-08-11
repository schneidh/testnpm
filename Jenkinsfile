pipeline {
    agent {
        docker 'node:7-onbuild'
    }
    stages {
      stage("a") {
        docker.image('node:7').withRun('-u root') {
          sh 'npm install'
        }
      }
    }
}
