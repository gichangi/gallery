pipeline { 
  agent any
  tools { 
    nodejs "Node19"
  }
      environment{
          RENDER_KEY = credentials('render-key')
      }
  stages { 
    stage('clone repository') {
      steps { 
        git 'https://github.com/gichangi/gallery'
      }
    }
    stage('Install') {
      steps { 
        sh 'npm install'
      }
    }
    stage('test') {
      steps { 
        sh 'npm test'
      }
    }
    stage('deploy') {
      steps { 
        sh 'curl -X POST https://api.render.com/deploy/${RENDER_KEY}'
      }
    }
    
  }
  post {
    success {
      slackSend color: 'good', message: 'Build #'+BUILD_NUMBER+' was successfully deployment on https://gallery-jenkins.onrender.com/'
    }
    failure {
        mail body: 'Failed Build #'+BUILD_NUMBER+'',  subject: 'Error Build #'+BUILD_NUMBER+'', to: 'john.gichangi@student.moringaschool.com'
    }
  }
}