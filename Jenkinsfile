pipeline{
    agent any 
    
    stages{
        stage('SCM') {
            steps{
                cleanWs()
                git branch: 'main', url: 'https://github.com/Siddeshg672/hello_world_public_war.git'
            }
        }
        stage('compile'){
            steps{
                sh "mvn clean install"
                sh "docker build -t dockeruplaod:${BUILD_NUMBER} -f Dockerfile ."
                 sh "docker tag dockeruplaod:${BUILD_NUMBER} kumarcc1/tomcat:${BUILD_NUMBER}"
                 withCredentials([usernamePassword(credentialsId: 'dockercred', passwordVariable: 'pass', usernameVariable: 'user')]) {
                sh "docker login -u ${user} -p ${pass} create.jfrog.io"
                sh "docker push  kumarcc1/tomcat:${BUILD_NUMBER}"
                 }
                
            }
        }
         stage('create container'){
            steps{
                script{
                withCredentials([usernamePassword(credentialsId: 'dockercred', passwordVariable: 'pass', usernameVariable: 'user')]) {
                    sh "docker login -u ${user} -p ${pass} create.jfrog.io"
                    sh "docker pull kumarcc1/tomcat:${BUILD_NUMBER}"
                    
                    sh "docker run -id --name tomcat -p 8090:8080  kumarcc1/tomcat:${BUILD_NUMBER}"
                }
                    
                }
            }
        }
        
        
    }
}
