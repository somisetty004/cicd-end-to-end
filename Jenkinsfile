pipeline {
    
    agent any 
    
    environment {
        dockerimage = ''
        registry = 'somisetty/python-pipeline'
        registrycredentials = 'somisetty-dockerhub'
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
                    dockerimage = docker.build registry
                }
            }
        }

        stage('Push the artifacts'){
           steps{
                script{
                    docker.with registry( '', registrycredentials ) {
                    dockerimage.push()
                }
            }
        }
    }
}
    
