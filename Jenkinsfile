pipeline {
    agent {
        docker {
          image 'node:7-onbuild'
          args '-u root'
        }
    }
    stages {
      stage("a") {
        steps {
          sh 'npm install'
        }
      }
    }
}
