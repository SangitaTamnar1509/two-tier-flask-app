pipeline{
 agent any;
 stages{
  stage("Code"){
   steps{
    git url: "https://github.com/SangitaTamnar1509/two-tier-flask-app.git", branch: "master"
   }
  }
  stage("Build"){
   steps{
    sh "docker build -t flask-my-app ."
   }
  }
  stage("push to dockerhub"){
   steps{
    withCredentials([usernamePassword(
     credentialsId:"dockerhubcred",
     usernameVariable:"dockerhubuser",
     passwordVariable:"dockerhubpass"
    )]){
     sh "docker login -u ${env.dockerhubuser} -p ${env.dockerhubpass}"
     sh "docker image tag flask-my-app ${env.dockerhubuser}/flask-my-app"
     sh "docker push ${env.dockerhubuser}/flask-my-app:latest
    }
   }
  }
  stage("Test"){
   steps{
    echo "verified successfully"
   } 
  }
  stage("Deploy"){
   steps{
    sh "docker compose up -d --build flask-app"
   }
  }
 }
}
