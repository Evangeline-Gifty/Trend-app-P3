pipeline {
  agent any

  stages {
    stage('Clone Repo') {
      steps {
        git branch: "${BRANCH_NAME}",
        url: 'https://github.com/Evangeline-Gifty/Trend-app-P3.git'
      }
    }

    stage('Build Image') {
      steps {
        sh './build.sh'
      }
    }

    stage('Push Image') {
      steps {
        script {
          if (env.BRANCH_NAME == 'dev') {
            sh '''
              docker tag trend-app evangelinegiftyy/trend-app-dev:latest
              docker push evangelinegiftyy/trend-app-dev:latest
            '''
          }
          if (env.BRANCH_NAME == 'master') {
            sh '''
              docker tag trend-app evangelinegiftyy/trend-app-prod:latest
              docker push evangelinegiftyy/trend-app-prod:latest
            '''
          }
        }
      }
    }
  }
}
