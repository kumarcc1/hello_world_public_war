pipeline{
    agent any
    stages{
        stage('checkout'){
           steps{
               git branch: 'main', url: 'https://github.com/Siddeshg672/hello_world_public_war.git'
           } 
        }
        
        stage('create binaries'){
            steps{
                sh "mvn clean install"
                }
        }
        stage('create docker image'){
            steps{
                sh "docker build -t kumara/devopsapp:latest ."
                sh "docker tag kumarcc1/devopsapp:latest kumara/devopsapp:test-deploy_${BUILD_NUMBER}"
                sh "docker push kumarcc1/devopsapp:test-deploy_${BUILD_NUMBER}"
                
            }
        }
    }
}
