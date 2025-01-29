pipeline {
  agent any
  stages {
    stage('build Stage') {
      steps {
        git(url: 'https://github.com/techhubpr/jrepo1', branch: 'main', credentialsId: 'eb48dc0e-21bb-43f1-9f0b-12efca9e64c2')
        sh '''sudo docker rm -f $(sudo docker ps -aq)||true && sudo docker rmi -f $(sudo docker images -aq)
sudo docker build -t jenkinsrb/cirepo1:latest .
sudo docker push jenkinsrb/cirepo1:latest'''
      }
    }

    stage('DEV & QA') {
      parallel {
        stage('Deploy to DEV') {
          steps {
            sh '''sudo docker rm -f $(sudo docker ps -aq)||true && sudo docker rmi -f $(sudo docker images -aq)
sudo docker run -d -p 7777:80 --name con1 jenkinsrb/cirepo1:latest
'''
          }
        }

        stage('Deploy to QA') {
          steps {
            echo 'QA done'
          }
        }

      }
    }

    stage('Deploy to Prod') {
      steps {
        echo 'Prod Done'
      }
    }

  }
}