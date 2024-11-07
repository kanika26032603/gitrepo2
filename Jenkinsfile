pipeline {
  agent any
  stages {
    stage('SCM') {
      steps {
        git(url: 'https://github.com/kanika26032603/gitrepo2', branch: 'main', credentialsId: 'a82e4c87-93a7-4e48-9974-215d9cf8cfcd')
      }
    }

    stage('Build&Publish') {
      steps {
        sh '''sudo docker build -t kanika297/srepo1:latest
 .sudo docker push kanika297/srepo1:latest '''
      }
    }

    stage('Deploy') {
      parallel {
        stage('DeployDev') {
          steps {
            sh '''sudo docker rm -f $(sudo docker ps -aq)|true
sudo docker run -d -p 7777:80 --name devcon1 kanika297/srepo1:latest'''
          }
        }

        stage('DeployQA') {
          steps {
            sh '''sudo docker rm -f $(sudo docker ps -aq)|true
sudo docker run -d -p 9999:80 --name qacon1 kanika297/srepo1:latest'''
          }
        }

      }
    }

  }
}