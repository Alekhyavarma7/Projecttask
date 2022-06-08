pipeline{
agent any
tools {

}
environment {
dockerhub=credentials('dockerhub')
}
stage('build image')
when{
branch "prod"
steps{
sh 'docker build -t Nodejs-app:1.01 .'
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