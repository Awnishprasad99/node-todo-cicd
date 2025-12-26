@Library("Shared") _
pipeline{
    agent { label 'dev-server' }
    
    stages{
        stage("Code Clone"){
            steps{
                script{
                echo "Code Clone Stage."
                clone("https://github.com/Awnishprasad99/node-todo-cicd.git", branch: "master")
                }
               
            }
        }
        stage("Trivy file system scan"){
            steps{
                script{
                    trivy_fs()
                }
            }
        }
        stage("Code Build & Test"){
            steps{
                echo "Code Build Stage."
                sh "docker build -t node-app ."
            }
        }
        stage("Push To DockerHub"){
            steps{
                script{
                    docker_push("dockerHubCreds", "two-tier-flask-app")
                }
                }
            }
        }
        stage("Deploy"){
            steps{
                sh "docker compose down && docker compose up -d --build"
            }
        }
    }
}
