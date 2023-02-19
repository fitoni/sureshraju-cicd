pipeline {
    agent any
    tools{
        maven 'maven'
    }
    
    stages{
        stage('Build Maven'){
            steps{
                script{
                    sh 'mvn clean install'
                }
            }
        }

        stage('Build Docker Image'){
            steps{
                script{
                    sh 'docker build -t fitoni/sureshrajuvetukuri .'                    
                }
            }
        }

         stage('Push Docker Image onto Hub'){
            steps{
                script{
                     withCredentials([string(credentialsId: 'dockerhubpassword', variable: 'dockerhubpassword')]) {
                        sh 'echo $dockerhubpassword | docker login -u fitoni --password-stdin https://index.docker.io/v1/'                        
                    } 
                    sh 'docker push fitoni/sureshrajuvetukuri'
                }
            }
        }

        /*  stage('Deploy to Kubernetes Cluster'){
            steps{
                script{
                    kubernetesDeploy (configs: 'deploymentservice.yaml', kubeconfigId: 'kubeconfig')
                }
            }
        }  */
    }
}
