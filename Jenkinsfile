pipeline {
    agent any
    environment {
        DOCKER_HUB_CREDENTIALS = 'dockerhub_credential' // 确保这个 ID 与 Jenkins 凭据配置中的一致
    }
    stages {
        stage('Package') {
            steps {
                checkout scm
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Building image') {
            steps {
                script {
                    docker.build('12110416781/title:latest')
                }
            }
        }
        stage('Upload image') {
            steps {
                script {
                    docker.withRegistry('', DOCKER_HUB_CREDENTIALS) {
                        docker.image('12110416781/title:latest').push()
                    }
                }
            }
        }
        stage('Run containers') {
            steps {
                script {
                    docker.image('12110416781/title:latest').run('-p 10084:8080')
                    docker.image('12110416781/title:latest').run('-p 10085:8080')
                    docker.image('12110416781/title:latest').run('-p 10086:8080')
                }
            }
        }
    }
}
