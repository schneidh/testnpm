pipeline {
    agent {
        docker 'node'
    }
    stages {
        stage("check node") {
            steps {
                sh 'node --version && npm --version'
            }
        }
    }
}
