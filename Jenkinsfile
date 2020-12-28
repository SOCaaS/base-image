pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                sh 'echo ${BUILD_NUMBER}'
                sh 'docker build --tag base/ubuntu:latest ./ubuntu'
                sh 'docker build --tag base/ubuntu-supervisor:latest ./ubuntu-supervisor'
                sh 'docker build --tag base/terraform:latest ./terraform'
                sh 'docker build --tag base/openstack-client:latest ./openstack-client'
           }
        }
        stage('CleanUp') {
            steps {
                echo "Cleaning Up"
                sh 'docker image prune -f'
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