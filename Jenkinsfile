pipeline {
  agent any
  tools {
    maven 'M2_HOME'
        }
stages {
   stage('Git Checkout') {
      steps {
        git 'https://github.com/belosheabhijeet/MyFinalProject-Insured-Me.git'
           }
       }
   stage('Build Package') {
       steps {
         sh 'mvn package'
       }
  }
   stage('Publish HTML Reports') {
     steps {
       publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: '/var/lib/jenkins/workspace/Insured-Me-Project/target/surefire-reports', reportFiles: 'index.html', reportName: 'HTML Report', reportTitles: '', useWrapperFileDirectly: true])
           }
                               }

   stage('Created docker image') {
     steps {
       sh 'docker build -t belosheabhijeet/insureme-app:1.0 .'
        }       
         }
   stage('Push the image to dockedr hub') {
     steps {
       withCredentials([usernamePassword(credentialsId: 'docker1-hub', passwordVariable: 'docker_password', usernameVariable: 'docker_user')]) {
     sh 'docker login -u ${docker_user} -p ${docker_password}'
        }
        sh 'docker push belosheabhijeet/insureme-app:1.0'
     }
       }
           }
}
