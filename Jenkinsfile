pipeline {
    agent {
        docker 'node:7-onbuild'
    }
    stages {
        stage("check node") {
            steps {
                sh 'npm install'
            }
        }
    }
}
