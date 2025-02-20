pipeline {
    agent any
    parameters {
        choice(name: 'ACTION', choices: ['apply', 'destroy'], description: 'Select the action')
    }
    environment {
        AWS_ACCESS_KEY_ID = credentials('AWS_ACCESS_KEY_ID')
        AWS_SECRET_ACCESS_KEY = credentials ('AWS_SECRET_ACCESS_KEY')

    }
    stages {
        stage('git clone') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/PrashanthMunigala/mydemoapp.git']])
            }
        }
        stage('build backend') {
            steps {
                    sh 'terraform init'
                }
        }
         stage('build backend plan') {
            steps {
                    sh 'terraform plan'
                }
        }
        stage('backend terraform apply or destroy') {
            steps {
                script {
                    if (params.ACTION == 'apply') {
                            sh 'terraform apply -auto-approve'
                    } 
                    else if (params.ACTION == 'destroy') {
                            sh 'terraform destroy -auto-approve'
                    }
                }
            }
        }
    }
}
