pipeline{
    agent any
    stages{
       stage('Building image') {
      steps{
        script {
          withCredentials([usernamePassword(credentialsId: 'docker', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]){
            sh "docker build -t ${USERNAME}/helthtracker  ."
            sh "echo ${PASSWORD} | docker login -u ${USERNAME} --password-stdin"
            sh "docker push ${USERNAME}/notebook"
        }
      }
    }
       stage('Deploy Image') {
      steps{
         script {
            withCredentials([usernamePassword(credentialsId: 'docker', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]){
            sh "docker run -d --name HelthTracker -p 3000:3000  ${USERNAME}/notebook"
            sh "docker image prune -a -f"
        }
        }
      }
    }
}
}
}
