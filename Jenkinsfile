pipeline {
    agent {
        node {
            label 'agent-1'
        }
    }
    options {
        ansiColor('xterm')
    }
    parameters {
        choice(name: 'action', choices: ['apply', 'destroy'], description: 'Pick something')
    }
    stages {
        stage('terraform init') {
            steps { 
                sh """
                    terraform init
                """
            }
        }
        stage('terraform plan') {
            steps { 
                sh "terraform plan"
            }
        }
        stage('terraform Deploy') {
            when {
                expression{
                    params.action =="apply"
                } 
            }
            input {

                message 'should we continue?'
                ok "you shou continue"
            }
            steps{
                sh "terraform apply -auto-approve"
            }
        }
        stage('terraform destroy') {
            when {
                expression{
                    params.action =="destroy"
                } 
            }
            input {
                message 'should we continue?'
                ok "you shou continue destroy"
            }
            steps{
                sh "terraform destroy -auto-approve"
            }
        }
    }
    post { 
        always { 
            echo 'I will always say Hello again!'
        }
        failure { 
            echo 'this runs when pipeline is failed, used generally to send some alerts'
        }
        success{
            echo 'I will say Hello when pipeline is success'
        }
    }
}