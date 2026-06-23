pipeline{
 agent { label "dev"};
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
     sh "docker push ${env.dockerhubuser}/flask-my-app:latest"
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
 post{
  success{
   script{
    emailext from: 'stamnar140@gmail.com',
    to: 'stamnar140@gmail.com',
    body: 'Build success CICD app',
    subject: 'Build success for demo CICD app'
   }
  }
  failure{
   script{
    emailext from: 'stamnar140@gmail.com',
    to: 'stamnar140@gmail.com',
    body: 'Build Failed CICD app',
    subject: 'Build failed for demo CICD app'
   }
  }
 }
}
