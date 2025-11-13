pipeline {
    agent any
    stages{
        stage('Build Maven'){
            steps{
                //checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Java-Techie-jt/devops-automation']]])
                sh 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t k8/devops-integration:latest .'
                    sh 'docker tag k8/devops-integration:latest localhost:5000/k8/devops-integration:latest
                    sh 'docker push localhost:5000/k8/devops-integration:latest
                }
            }
        }
        stage('Deploy to k8s'){
            steps{
                script{
                   sh 'kubectl apply -f deploymentservice.yaml'
                }
            }
        }
    }
}
