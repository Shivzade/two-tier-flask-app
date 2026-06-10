@Library("Shared") _
pipeline{
    
    agent { label "dev"};
    
    stages{
        stage("Code Clone"){
            steps{
                script{
                    clone("https://github.com/Shivzade/two-tier-flask-app.git","master")
                }
            }
        }
        stage("Trivy File System Scan"){
            steps{
                script{
                    trivy_fs()
                }
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
                script{
                    docker_push("DockerHubCreds", "two-tier-flask-app")
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
