pipeline{
    
    agent { label "dev"};
    
    stages{
        stage("Code Clone"){
            steps{
                git url: "https://github.com/Shivzade/two-tier-flask-app.git", branch:"master"
            }
        }
        stage("Trivy File System Scan"){
            steps{
                sh "trivy fs . -o results.json"
            }
        }
        stage("Build"){
            steps{
                sh "docker build -t two-tier-flask-app . "
            }
            }
        
        stage("Test"){
            steps{
                echo "Developer/Tester write the test cases"
            }
            
        }
        stage("Push to Docker Hub"){
            steps{
                withCredentials([usernamePassword(
                    credentialsId: "DockerHubCreds",
                    usernameVariable: "dockerHubUser",
                    passwordVariable: "dockerHubPass"
                    )]){
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker image tag two-tier-flask-app ${env.dockerHubUser}/two-tier-flask-app"
                sh "docker push ${env.dockerHubUser}/two-tier-flask-app:latest"
                    }
            }
        }
        stage("Deploy"){
            steps{
                sh "docker compose up -d --build flask-app"
            }
            
        }
    }
    
post{
    success{
        script{
            emailext from: "shivkumarzade7446@gmail.com",
            to: "shivkumarzade7446@gmail.com",
            subject: "Build success for Demo CICD App",
            body: "Build success for Demo CICD App"
            
        }
    }
    failure{
        script{
            emailext from: "shivkumarzade7446@gmail.com",
            to: "shivkumarzade7446@gmail.com",
            subject: "Build Failed for Demo CICD App",
            body: "Build Failed for Demo CICD App"
            
        }
    }
}
}
