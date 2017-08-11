pipeline {
    agent {
        docker {
          image 'node'
          args ''
        }
    }
    environment {
      HOME = '.'
    }
    stages {
       stage("install and release") {
        steps {
          sh 'git config --global user.email "pipeline@example.com"'
          sh 'git config --global user.name "Pipeline"'
          checkout scm
          dir('otherRepo') {
            git url: 'http://git.repo.blah/RepoA.git' // clones repo A to subdir
          }
          sh 'npm install'
          sh 'npm version patch'
          sh './npm-extract-version.sh > version'
          withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'd61d369a-1dab-4ad0-82f6-0f8f2c6d0b57', usernameVariable: 'GIT_USERNAME', passwordVariable: 'GIT_PASSWORD']]) {
            sh('git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/schneidh/testnpm master:master')
            sh('git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/schneidh/testnpm --tags master:master')
          }
          script {
            env.version = readFile 'version'
          }
        }
      }
      stage("docker") {
        steps {
          sh "echo 'The version is ${env.version}'"
          dir('repoB') {
            git url: 'https://github.com/schneidh/struts2scopeplugin'
          }
          dir('repoC') {
            git url: 'https://github.com/fuhrysteve/php-docker-apache-example'
            def app = docker.build "tempdocker"
          }
        }
      }
    }
}
