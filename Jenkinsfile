pipeline{
    agent any
    stages{
        stage('Clone'){
            steps{
                git 'https://github.com/Ayush-pd07/POC-07.git'
            }
        }
        stage('Build Docker Image'){
            steps{
                sh 'docker build -t my-frontend ./frontend'
            }
        }
        stage('Deploy using Ansible'){
            steps{
                sh 'ansible-playbook ansible/deploy.yml -i ansible/inventory'
            }
        }
    }
}