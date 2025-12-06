@Library("shared-library") _
pipeline{
    agent {label "Vinod"}
    
    stages{
        stage("Hello"){
            steps{
                script{
                    hello()
                }
            }
        }
        stage("Code"){
            steps{
                script{
                    codeClone("https://github.com/ArunRajbhar-Code/python-project1.git","main")
                }
            }
            
        }
        stage("Build"){
            steps{
                echo "this is build "
                sh "docker build -t python-project1 ."
                sh "docker ps"
            }
            
        }
        stage("Test"){
            steps{
                echo "this is test "
            }
            
        }
        stage("Push to dockerhub"){
            steps{
                echo "Pushing the code in dockerhub"
                withCredentials([usernamePassword('credentialsId':"dockerHubCred",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker image tag python-project1:latest rajbhararun/python-project1:latest"
                sh "docker push rajbhararun/python-project1:latest"
                }
                
                
            }
        }
        stage("Deploy"){
            steps{
                echo "this is deploy "
                sh "docker run -d -p 8000:8000 python-project1"
            }
            
        }
    }
}
