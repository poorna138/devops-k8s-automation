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
                    sh '"
                        eval $(minikube docker-env)
                        docker build -t k8/devops-integration .
                       '"
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
