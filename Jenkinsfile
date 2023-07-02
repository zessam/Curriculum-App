pipeline {
  agent any
  stages {
    stage('Checkout Code') {
      steps {
        git(url: 'https://github.com/zezo-rgb/Curriculum-App', branch: 'main')
      }
    }

    stage('Log') {
      parallel {
        stage('Log') {
          steps {
            sh '''ls -la 
'''
          }
        }

        stage('Frontend Unit Tests / Shell Script') {
          steps {
            sh 'cd curriculum-front && npm i && npm run test:unit'
          }
        }

      }
    }

    stage('Build Step') {
      steps {
        sh 'docker build -f curriculum-front/Dockerfile . '
      }
    }

    stage('Log into Dockerhub / Shell Script') {
      environment {
        DOCKERHUB_USER = 'zezo001'
        DOCKERHUB_PASSWORD = 'Z01015694287z'
      }
      steps {
        sh 'Docker -u $DOCKERHUB_USER -p $DOCKERHUB_PASSWORD'
      }
    }

  }
}