pipeline {
    agent any
    parameters {
        choice(name: 'action', choices: ['apply', 'destroy'], description: 'Select Terraform action (apply or destroy)')
    }
    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/stephane']], userRemoteConfigs: [[url: 'https://github.com/stephanemiafo/myvpctest.git']]])
            }
        }
        stage("Terraform init") {
            steps {
                sh 'terraform init'
            }
        }
        stage("Terraform Action") {
            steps {
                script {
                    echo "Terraform action from the parameter is ${params.action}"
                    sh "terraform ${params.action} -auto-approve -no-color"
                }
            }
        }
    }
}
