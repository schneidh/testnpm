pipeline {
    agent {
        docker 'node'
    }
    stages {
        stage("check node") {
            steps {
                sh 'npm install'
            }
        }
    }
}
