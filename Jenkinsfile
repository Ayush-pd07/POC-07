pipeline {
  agent any
 
  environment {
    REGION = "eu-north-1"
    ECR_URI = "606664404429.dkr.ecr.eu-north-1.amazonaws.com/frontend-app"
  }
 
  stages {
    stage('Build Docker Image') {
      steps {
        sh 'docker build -t frontend-app ./frontend'
      }
    }
 
    stage('Login to ECR') {
      steps {
        sh '''
        aws ecr get-login-password --region $REGION | \
        docker login --username AWS --password-stdin $ECR_URI
        '''
      }
    }
 
    stage('Tag Image') {
      steps {
        sh 'docker tag frontend-app:latest $ECR_URI:latest'
      }
    }
 
    stage('Push to ECR') {
      steps {
        sh 'docker push $ECR_URI:latest'
      }
    }
 
    stage('Deploy using Ansible') {
      steps {
        sh '''
        ansible-playbook ansible/deploy.yml \
        -i ansible/inventory \
        --extra-vars "ecr_uri=$ECR_URI"
        '''
      }
    }
  }
}
 