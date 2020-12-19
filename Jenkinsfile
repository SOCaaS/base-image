pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                sh 'echo ${BUILD_NUMBER}'
                sh 'docker build --tag base/ubuntu:latest ./ubuntu'
           }
        }
    }
    post {
        success {
            discordSend description: "Build Success", footer: "Base Image", link: env.BUILD_URL, result: currentBuild.currentResult, title: JOB_NAME, webhookURL: env.SOCAAS_WEBHOOK
        }
        failure {
            discordSend description: "Build Failed", footer: "Base Image", link: env.BUILD_URL, result: currentBuild.currentResult, title: JOB_NAME, webhookURL: env.SOCAAS_WEBHOOK
        }
    }
}