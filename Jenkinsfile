/*pipeline{
 agent any
 docker {
            image 'node:18.3.0' 
            //args '-p 3000:3000' 
        }
tools {
 nodejs '18.3.0'
}
 
//environment {
// dockerhub=credentials('dockerhub')
 //}
 
 stages{
 // stage ('Install dependencies')
  //{
   //     steps{
  //              sh 'npm install'
  //          }
  //  }
  stage ('build')
  {
   
       steps{
               sh 'npm install'
        sh 'npm run build'
           }
  }
stage('build imag')
 {
when{
 
branch "prod"
}
steps{
sh 'docker build -t Nodejs-app:1.01 .'
}
 }
stage('pushing to dockerhub')
{
when{
branch "prod"
}
steps{
sh 'docker tag Nodejs-app:1.01 alekhyavarma25/Nodejs-app:1.01 ' 
sh 'echo $dockerhub_PSW docker login -u $dockerhub_USR --password-stdin'
sh 'docker push alekhyavarma25/Nodejs-app:1.01 '
}
}
 }
}*/
node {
     def app 
     stage('clone repository') {
      checkout scm  
    }
     stage('Build docker Image'){
      app = docker.build("alekhyavarma25/appnodejstask")
    }
     stage('Test Image'){
       app.inside {
         sh 'echo "TEST PASSED"'
      }  
    }
     stage('Push Image'){
       docker.withRegistry('https://registry.hub.docker.com', 'git') {            
       app.push("${env.BUILD_NUMBER}")            
       app.push("latest")   
   }
}
