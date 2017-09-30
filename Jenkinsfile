pipeline {
    agent { node { label 'master' } }
    tools {nodejs "NODE6_11_3"}
    stages {
       stage("setup") {
          steps {
            sh "node -v"
            sh "npm -vaaba"
          }
       }
       stage("build") {
         steps {
           sh 'export PATH=$PATH:$NODEJS'
           sh 'rm -rf node_modules'
           sh 'npm install'
         }
       }
    }
    post {
      failure {
        echo("FAILED Build Number $BUILD_NUMBER ${currentBuild?.result}")
      }
      unstable {
      }
      aborted {
      }
      changed {
         script {
            if (currentBuild?.result == 'SUCCESS') {
              echo "back to normal $BUILD_NUMBER ${currentBuild?.result}"
            }
        }
      }
    }
}
