pipeline {
    agent { node { label 'master' } }
    tools {nodejs "NODE6_11_3"}
    stages {
       stage("setup") {
          steps {
            checkout scm
            dir('repoC') {
              git url: 'https://github.com/fuhrysteve/php-docker-apache-example'
            }
            sh "node -v"
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
          sh 'git config --global user.email "pipeline@example.com"'
          sh 'git config --global user.name "Pipeline"'
          sh 'npm version patch'
          sh './npm-extract-version.sh > version'
          withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: '93bdcceb-590a-404f-967e-1e734cdacaca', usernameVariable: 'GIT_USERNAME', passwordVariable: 'GIT_PASSWORD']]) {
            sh('git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/schneidh/testnpm master:master')
            sh('git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/schneidh/testnpm --tags master:master')
          }
          script {
            env.version = readFile 'version'
          }
        }
      }
    }
}
