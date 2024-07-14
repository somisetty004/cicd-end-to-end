pipeline {
    
    agent any 
    
    environment {
        DOCKERHUB_CREDENTIALS = credentials('somisetty-dockerhub')
    }
    
    stages {
        
        stage('Checkout'){
           steps {
                git credentialsId: '849704bf-a5da-49e5-86a1-12fb3c4beae4', 
                url: 'https://github.com/somisetty004/cicd-end-to-end.git',
                branch: 'main'
           }
        }

        stage('Build Docker'){
            steps{
                script{
                    sh '''
                    echo 'Buid Docker Image'
                    docker build -t somisetty/python-pipeline:latest .
                    '''
                }
            }
        }

        stage('Push the artifacts'){
           steps{
                script{
                    sh '''
                    echo 'Push to Repo'
                    docker push somisetty/python-pipeline:latest
                    '''
                }
            }
        }
    }
}   
    
