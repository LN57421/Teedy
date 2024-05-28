pipeline {
    agent any
    stages {
        stage('Package') {
            steps {
                checkout scm
                sh 'mvn -B -DskipTests clean package'
            }
        }
        // Building Docker image
        stage('K8s') {
            steps {
                sh 'kubectl set image deployments/hello-node docs=title/traccytian:latest'
            }
        }
    }
}
