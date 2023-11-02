node('appserver')
{
  def app

  stage ('Cloning GitHub URL')
  {
    checkout scm
  }        
  stage ('Build-and-Tag Image')
  {
    app = docker.build("dchirwa/node-js-qr-code-generator:latest")
  }        
  stage ('Post-to-DockerHub')
  {
    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub_credentials')
    {
      app.push("latest")
    }
  }        
  stage ('Pull-Image-Server')
  {
    sh "docker-compose down"
    sh "docker-compose up -d"
  }
        
}
