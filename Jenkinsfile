pipeline{
    agent any
    stages{
        stage("clone"){
            steps {
                echo "clone code from github"
                git url:"https://github.com/mohsinkhanstc220/coffee-shop.git",branch: "main"
            }
        }
        stage("build"){
            steps {
                echo "build the code stage"
                //sh "docker build -t my-coffee-shop ."
            }
        }
        stage("push"){
            steps {
                echo "push the image to docker hub"
                withCredentials([usernamePassword(credentialsId:"docker-hub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                    //sh "docker tag my-coffee-shop ${env.dockerHubUser}/my-coffee-shop:v3"
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                   // sh "docker push ${env.dockerHubUser}/my-coffee-shop:v3"
                }
            }
        }
        stage("deploy"){
            steps {
                echo "deploy the image on server"
                //sh "docker-compose down && docker-compose up -d"
                //sh "docker run -d -p 8088:80 --name my-new-coffee-shop mohsinkhan2220/my-coffee-shop:v3 "
                sh "kubectl apply -f kubefile.yml --kubeconfig=/var/lib/jenkins/.kube/config"
                
            }
        }
    }
}
