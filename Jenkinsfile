pipeline {
    agent {
        docker 'node:7-onbuild'
        args '-u root'
    }
    stages {
      stage("a") {
        sh 'npm install'
      }
    }
}
