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
        
        stage('Checkout K8S manifest SCM'){
            steps {
                git credentialsId: '849704bf-a5da-49e5-86a1-12fb3c4beae4', 
                url: 'https://github.com/somisetty004/Cicd-deployment-files.git',
                branch: 'main'
            }
        }
        
        stage('Update K8S manifest & push to Repo'){
            steps {
                script{
                    withCredentials([usernamePassword(credentialsId: '849704bf-a5da-49e5-86a1-12fb3c4beae4', passwordVariable: 'somisetty@123', usernameVariable: 'somisetty004')]) {
                        sh '''
                        cat deploy.yaml
                        sed -i '' "s/32/${BUILD_NUMBER}/g" deploy.yaml
                        cat deploy.yaml
                        git add deploy.yaml
                        git commit -m 'Updated the deploy yaml | Jenkins Pipeline'
                        git remote -v
                        git push https://github.com/somisetty004/Cicd-deployment-files.git HEAD:main
                        '''                        
                    }
                }
            }
        }
    }
}
