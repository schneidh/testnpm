pipeline {
    agent { node { label 'master' } }
    tools {nodejs "NODE6_11_3"}
    stages {
       stage("setup") {
          steps {
            sh "node -v"
            sh "npm -v"
          }
       }
       stage("build") {
         steps {
           sh 'export PATH=$PATH:$NODEJS'
           sh 'rm -rf node_modules'
           sh 'npm install'
         }
       }
       stage("release") {
        steps {
          sshagent (credentials: ['testnpm-ssh']) {
            sh 'git config --global user.email "jenkins@doradosystems.com"'
            sh 'git config --global user.name "Jenkins Release"'
            sh 'npm version patch'
            sh('git push origin --tags master:master')
          }
        }
      }
      stage("merge to develop") {
        steps {
          sshagent (credentials: ['testnpm-ssh']) {
            sh 'git config --global user.email "jenkins@doradosystems.com"'
            sh 'git config --global user.name "Jenkins Release"'
            sh('git checkout -B develop origin/develop')
            sh('git merge master')
            sh('git push origin develop:develop')
          }
        }
      }
    }
    post {
      failure {
        echo("FAILED Build Number $BUILD_NUMBER ${currentBuild?.result}")
      }
      unstable {
        echo("UNSTABLE Build Number $BUILD_NUMBER ${currentBuild?.result}")
      }
      aborted {
        echo("ABORTED Build Number $BUILD_NUMBER ${currentBuild?.result}")
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
